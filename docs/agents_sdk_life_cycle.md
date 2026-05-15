# OpenAI Agents SDK — Life Cycle

## Overview

This document describes the principles and sequential life cycle of the multi-agent system defined in this repository, with a focus on how each stage maps to OpenAI Agents SDK constructs.

The system transforms a high-level user intent into a validated, executed, and observed workflow by composing SDK `Agent` objects, runner invocations, tool calls, handoffs, guardrails, and lifecycle hooks into a deterministic pipeline.

---

## Core Principles

### 1. Intent-Driven Planning
Every workflow begins with an explicit user intent (`TaskIntent`). The system never infers what to do implicitly; the `PlannerAgent` converts intent into a concrete, inspectable `TaskGraph` before any execution starts.

### 2. Explicit Task Graph
Work is represented as a directed graph of `TaskStep` entries. Each step carries its own agent specification, tool list, expected output contract, and dependency references. This makes the plan auditable, retryable, and traceable before the first token is generated.

### 3. Policy-First Execution
No step executes until the `PolicyGate` has validated the full graph against safety rules, budget constraints, handoff restrictions, and approval requirements. Compliance is enforced structurally, not as an afterthought.

### 4. Agent Modularity
Every agent — Planner, Orchestrator, Worker, Critic, HITL — is an isolated SDK `Agent` instance with its own `instructions`, `tools`, `output_type`, `guardrails`, and optional `handoffs`. Agents do not share mutable state; communication happens through structured data contracts.

### 5. Composable Handoffs and Tool Calls
Orchestration is achieved through SDK-native mechanisms: `handoffs` for delegating control between agents, and `tools` for invoking external systems. Workers are registered as handoff targets or as callable tools, depending on the delegation model chosen for each step.

### 6. Continuous Observation
An `Observer/Critic` agent evaluates every completed step using the SDK's tracing hooks and run results. Quality feedback is fed back into re-planning when necessary, closing a refinement loop before results are considered final.

### 7. Human-in-the-Loop by Design
HITL is a first-class stage, not an escape hatch. Whenever the `PolicyGate` or `Orchestrator` detects a high-risk or ambiguous decision, execution is paused and a structured review request is surfaced to a human reviewer.

### 8. Unified Tracing
The SDK's built-in tracing captures every run, span, tool invocation, handoff event, and lifecycle hook call. Trace data is the shared evidence layer used by the `Observer`, the `Orchestrator`, and any downstream auditing or optimization tooling.

---

## Life Cycle Flow

```
User Intent
    │
    ▼
[1] TaskIntent
    │   (structured goal with constraints)
    ▼
[2] PlannerAgent  ──►  TaskGraph
    │   (SDK Agent: LLM + structured output)
    ▼
[3] PolicyGate
    │   (validate: budget, safety, approvals)
    │
    ├── REJECT / REVISE  ──► back to PlannerAgent
    │
    └── APPROVE
         │
         ▼
[4] Orchestrator
    │   (SDK Agent: step scheduler + state tracker)
    │
    ├── [5] Worker Agent(s)
    │       (SDK Agent: tools + handoffs per step)
    │       │
    │       └── result artifacts
    │
    ├── [6] Observer / Critic
    │       (SDK Agent: evaluation + trace review)
    │       │
    │       ├── PASS  ──► next step
    │       └── FAIL  ──► re-plan or retry
    │
    ├── [7] HITL (when required)
    │       (human review + decision)
    │
    └── [8] Tracing & Observability
            (spans all stages, always active)
```

---

## Sequential Life Cycle Stages

### Stage 1 — TaskIntent

**What it is**: The entry point of the system. A `TaskIntent` object carries the raw user goal, normalized intent text, optional constraints (time budget, risk tolerance, output format), and a short description of the expected outcome.

**SDK mapping**: The intent is the input passed to the first `Runner.run()` call that targets the `PlannerAgent`. It is encoded as the initial user message or as a structured input that matches the agent's expected `input_type`.

**Outputs**: A validated `TaskIntent` object forwarded to the `PlannerAgent`.

---

### Stage 2 — PlannerAgent → TaskGraph

**What it is**: The `PlannerAgent` is an SDK `Agent` configured with a structured `output_type` that produces a `TaskGraph`. The graph contains an ordered or dependency-linked list of `TaskStep` entries. Each step specifies the agent role required, its tools, its inputs, and its expected output contract.

**SDK mapping**:
- Defined as `Agent(name="PlannerAgent", instructions=PLANNER_PROMPT, output_type=TaskGraph, tools=[...])`
- Invoked via `Runner.run(planner_agent, input=task_intent)`
- Structured output is validated against the `TaskGraph` schema before proceeding

**Outputs**: A `TaskGraph` passed to the `PolicyGate`.

---

### Stage 3 — PolicyGate

**What it is**: A validation layer that inspects the full `TaskGraph` before any worker is invoked. It checks budget compliance, safety rules, required human approvals, and handoff restrictions. The outcome is either APPROVE, PAUSE-FOR-APPROVAL, or REJECT-AND-REVISE.

**SDK mapping**:
- Implemented as a standalone policy function or a lightweight `Agent` with guardrail-style output
- Can leverage SDK input guardrails applied before the `Orchestrator` receives the graph
- Rejection triggers a feedback message back to the `PlannerAgent` for graph revision

**Outputs**: A `PolicyDecision` containing risk level, approval status, and any blocking findings.

---

### Stage 4 — Orchestrator

**What it is**: The `Orchestrator` is the coordination layer. It reads the validated `TaskGraph`, determines which steps are ready to execute (respecting dependencies), delegates each step to the appropriate Worker Agent, and tracks the state of every step through its lifecycle (`pending → in_progress → completed / failed`).

**SDK mapping**:
- Defined as `Agent(name="Orchestrator", instructions=ORCHESTRATOR_PROMPT, tools=[worker_tools], handoffs=[worker_agents])`
- Uses SDK `handoffs` to transfer control to Worker Agents when a step begins
- Uses SDK lifecycle hooks (`on_handoff`, `on_tool_call`) to update step states in the `TaskGraph`

**Outputs**: Updated `TaskGraph` with in-progress and completed step records.

---

### Stage 5 — Worker Agents

**What it is**: Worker Agents are specialized SDK `Agent` instances, each responsible for exactly one well-bounded domain action — such as web search, code execution, data retrieval, content generation, or API interaction. They receive the inputs defined by their `TaskStep`, execute using their configured tools, and return a structured result.

**SDK mapping**:
- Each worker is `Agent(name="<Role>Worker", instructions=WORKER_PROMPT, tools=[...], output_type=WorkerResult)`
- Invoked by the `Orchestrator` via a handoff or a tool call
- Guardrails on the worker validate both the inputs received and the outputs produced
- Results are returned to the `Orchestrator` as structured `WorkerResult` objects

**Outputs**: `WorkerResult` containing the step outcome, tool activity log, and trace reference.

---

### Stage 6 — Observer / Critic Evaluation

**What it is**: After each step (or batch of steps) completes, the `Observer` agent evaluates quality. It reviews the worker's output against the step's expected output contract, inspects trace data for anomalies, and emits a verdict. Weak or failed steps trigger a feedback loop back to the `PlannerAgent` for selective re-planning.

**SDK mapping**:
- Defined as `Agent(name="CriticAgent", instructions=CRITIC_PROMPT, tools=[trace_reader], output_type=EvaluationResult)`
- Uses the SDK tracing API to read span data from the completed step's run
- Emits `EvaluationResult` with `passed`, `quality_score`, `critique_notes`, and `retry_recommendation`

**Outputs**: `EvaluationResult` forwarded to the `Orchestrator` to decide continuation, retry, or re-planning.

---

### Stage 7 — Human-in-the-Loop (HITL)

**What it is**: HITL is activated when the `PolicyGate` flags an approval requirement or when the `Orchestrator` encounters a high-risk decision during execution. The workflow pauses and a structured review request is surfaced to a human reviewer. The human's decision — approve, reject, or modify — is injected back into the workflow as an explicit input.

**SDK mapping**:
- Implemented using SDK conversation continuation: the run is paused at a checkpoint, and a new `Runner.run()` is triggered once human input is received
- The HITL agent (`Agent(name="HITLAgent", ...)`) formats the context and available options for the reviewer
- Human responses are validated before resuming the `Orchestrator`

**Outputs**: A human decision record that unlocks the next pending step or triggers a plan revision.

---

### Stage 8 — Tracing & Observability

**What it is**: Tracing is always active across all stages. The SDK automatically captures trace identifiers, span events, tool call inputs/outputs, handoff transitions, lifecycle hook invocations, token usage, and execution timings. This data is the shared evidence layer for the `Observer`, debugging, auditing, and future workflow optimization.

**SDK mapping**:
- Built-in SDK tracing (`openai.agents.tracing`) captures all events automatically
- Custom `TracingProcessor` implementations can route data to external observability platforms
- Trace identifiers from each stage are attached to `TaskStep` records for end-to-end correlation

**Outputs**: Structured trace records available to all agents, the `Observer`, and external monitoring systems.

---

## Example

### Task: "Research the top 5 open-source vector databases and produce a comparison report"

#### Initial Task

A user submits the following intent:

> **Goal**: Research the top 5 open-source vector databases and produce a structured comparison report covering features, performance characteristics, licensing, and community activity.
> **Constraints**: Budget — 50,000 tokens; Output format — Markdown table + summary paragraph; Risk tolerance — low.

---

#### Agent Roles Required

| Role | Agent | Responsibility |
|------|-------|----------------|
| Planner | `PlannerAgent` | Decompose the intent into a `TaskGraph` of research and writing steps |
| Policy Enforcer | `PolicyGate` | Validate the graph against token budget and safety rules |
| Coordinator | `Orchestrator` | Schedule steps, delegate to workers, track progress |
| Researcher | `WebSearchWorker` | Search for information about each vector database |
| Analyst | `DataSynthesisWorker` | Extract and normalize feature data from search results |
| Writer | `ReportWriterWorker` | Compose the final Markdown comparison report |
| Quality Reviewer | `CriticAgent` | Evaluate each step's output for completeness and accuracy |
| Human Reviewer | `HITLAgent` | Approve the final report before delivery (flagged as required by policy) |

---

#### Execution Simulation

**Stage 1 — TaskIntent**
The user's goal is encoded into a `TaskIntent` object with the prompt text, token budget constraint, low risk tolerance flag, and expected Markdown output format. This object is passed to the `PlannerAgent`.

**Stage 2 — PlannerAgent → TaskGraph**
The `PlannerAgent` receives the `TaskIntent` and generates a `TaskGraph` with six `TaskStep` entries:
1. Search for top open-source vector databases (→ `WebSearchWorker`)
2. Search for performance benchmarks for each candidate (→ `WebSearchWorker`)
3. Search for licensing and community activity data (→ `WebSearchWorker`)
4. Synthesize and normalize all collected data (→ `DataSynthesisWorker`, depends on steps 1–3)
5. Write the Markdown comparison table and summary (→ `ReportWriterWorker`, depends on step 4)
6. Final human review of the report (→ `HITLAgent`, depends on step 5)

**Stage 3 — PolicyGate**
The `PolicyGate` inspects the graph:
- Token budget: estimated usage is within the 50,000-token limit → PASS
- Safety rules: no restricted content detected → PASS
- Approval requirement: step 6 is a HITL step flagged as required → recorded
- Decision: APPROVE with a pending HITL checkpoint at step 6

**Stage 4 — Orchestrator begins execution**
The `Orchestrator` identifies steps 1, 2, and 3 as independent (no dependencies) and dispatches them concurrently to three `WebSearchWorker` instances via SDK handoffs.

**Stage 5 — WebSearchWorker (steps 1, 2, 3)**
Each `WebSearchWorker` receives its search scope, calls the web search tool, and returns a `WorkerResult` containing the raw search findings and a trace reference. All three complete successfully.

**Stage 6 — CriticAgent evaluates steps 1–3**
The `CriticAgent` reviews the three results against the expected output contracts. It finds that step 2 returned sparse benchmark data for one database. It emits an `EvaluationResult` with a retry recommendation for step 2 only. The `Orchestrator` retries step 2 with a refined search query; the second attempt returns sufficient data.

**Stage 5 — DataSynthesisWorker (step 4)**
With steps 1–3 complete and validated, the `Orchestrator` dispatches the `DataSynthesisWorker`. It normalizes the collected data into a structured schema covering each database's features, performance notes, license type, and GitHub star count. Returns a `WorkerResult`.

**Stage 6 — CriticAgent evaluates step 4**
The `CriticAgent` confirms the synthesized data is complete and consistent across all five databases. Verdict: PASS.

**Stage 5 — ReportWriterWorker (step 5)**
The `Orchestrator` dispatches the `ReportWriterWorker` with the synthesized data. The worker produces a Markdown comparison table and a two-paragraph summary. Returns the formatted report as a `WorkerResult`.

**Stage 6 — CriticAgent evaluates step 5**
The `CriticAgent` checks the report for completeness, Markdown validity, and alignment with the original intent. Verdict: PASS with high quality score.

**Stage 7 — HITL (step 6)**
The `Orchestrator` reaches the HITL checkpoint. The `HITLAgent` formats a review request containing the full report, the quality score, and the critic's notes. The human reviewer approves the report without modifications.

**Stage 8 — Tracing throughout**
The SDK tracing layer has captured all events: six step spans, three web search tool calls (plus one retry), one synthesis tool call, one write tool call, two `CriticAgent` evaluation runs, and the HITL handoff event. Trace data is stored with end-to-end correlation IDs linking every span to the originating `TaskIntent`.

**Final output**: A validated, human-approved Markdown comparison report delivered back to the user, with a complete audit trail spanning all eight life cycle stages.

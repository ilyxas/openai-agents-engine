# Agents SDK Life Cycle

## Overview

This document defines the life cycle for executing complex tasks with the OpenAI Agents SDK in this repository.

The flow follows a controlled loop:

1. Receive user intent.
2. Convert intent into a structured execution plan.
3. Validate the plan against policies and runtime constraints.
4. Execute with specialized agents and tools.
5. Evaluate outcomes and decide whether to continue, retry, or re-plan.
6. Escalate to a human when policy or risk requires it.
7. Trace all actions for observability and post-run analysis.

## Core Principles

- **Single responsibility by role**: Planner, Orchestrator, Worker, Critic, and HITL roles stay logically separated.
- **Structured state**: Work is represented as explicit task steps with dependencies and status transitions.
- **Policy-first execution**: Validation happens before and during execution, not only at planning time.
- **Tool-bounded actions**: Workers operate through declared tools with scoped permissions.
- **Adaptive control loop**: Failures and critique feedback can trigger retries, branch changes, or re-planning.
- **Traceability by default**: Every lifecycle stage emits trace data for debugging and optimization.

## Life Cycle Flow

### 1. Task Intake

- Input: user goal, constraints, and optional context.
- Output: normalized `TaskIntent` for planning.
- SDK relevance: session memory keeps the interaction context and clarifications coherent.

### 2. Planning

- Agent role: **Planner Agent**.
- Action: transform `TaskIntent` into a `TaskGraph` with atomic `TaskStep` nodes.
- Output: ordered/dependency-aware execution graph including expected outcomes per step.

### 3. Policy and Feasibility Gate

- Component role: **PolicyGate**.
- Action: validate graph against budget, risk, safety, and required tool availability.
- Output: approved graph, rejected graph, or graph requiring revision.

### 4. Orchestration

- Agent role: **Orchestrator Agent**.
- Action: schedule executable steps, enforce dependencies, and route steps to worker roles.
- Output: runtime state transitions (`pending` → `in_progress` → `completed`/`failed`/`blocked`).

### 5. Step Execution

- Agent role: **Worker Agents**.
- Action: execute bounded tasks using declared tools (APIs, file tools, search, or utility functions).
- Output: structured step results, artifacts, and execution metadata.

### 6. Quality Evaluation

- Agent role: **Critic Agent**.
- Action: compare outputs to step acceptance criteria and policy expectations.
- Output: accept, request retry, request correction, or escalate for re-planning.

### 7. Human-in-the-Loop Decision Points

- Agent role: **HITL Agent / Human Reviewer**.
- Trigger conditions: high-risk actions, ambiguous intent, policy conflict, or unresolved critic feedback.
- Output: human approval, rejection, or guidance injected back into orchestration.

### 8. Recursion and Re-Planning

- Controller: **Orchestrator** in cooperation with **Planner**.
- Action: adjust graph for failed/changed conditions without restarting the whole process.
- Output: updated `TaskGraph` and resumed execution from the relevant checkpoint.

### 9. Completion and Delivery

- Action: aggregate validated outputs and prepare final response/artifacts.
- Output: user-facing result with clear completion status and unresolved items (if any).

### 10. Tracing and Post-Run Insights

- Component role: **Tracing**.
- Action: persist lifecycle events, handoffs, tool calls, retries, and approvals.
- Output: audit trail for diagnostics, quality tuning, and future optimization.

## Example: Initial Task and Execution Simulation

### Initial Task

"Create a pull request that adds `docs/agents_sdk_life_cycle.md`, updates the docs tree in `docs/architecture.md`, and keeps all repository content in English."

### Required Agent Roles

- **Planner Agent**: decomposes the request into documentation and structure-update steps.
- **Orchestrator Agent**: sequences execution and controls retries.
- **Worker Agent (Docs Author)**: writes the lifecycle document.
- **Worker Agent (Repo Editor)**: updates the repository tree section in architecture docs.
- **Critic Agent**: checks completeness, sequence clarity, and consistency with architecture constraints.
- **HITL Agent/Human**: resolves policy or scope ambiguity if detected.

### Required Tools

- Repository file read/write tools for markdown updates.
- Search tools to verify references and section consistency.
- Version-control reporting tools for progress and PR creation.
- Tracing utilities to capture lifecycle decisions and outcomes.

### Simulated Execution

1. **Task Intake**: User request is captured as a `TaskIntent` with constraints (only relevant docs changed, English-only output).
2. **Planning**: Planner generates steps:
   - Draft lifecycle documentation.
   - Add execution example with roles/tools.
   - Update architecture tree.
   - Validate and prepare PR.
3. **Policy Gate**: Plan passes because changes are documentation-scoped and within repository constraints.
4. **Orchestration**: Orchestrator dispatches writing and tree-update steps to documentation workers.
5. **Execution**:
   - Docs Author Worker produces `docs/agents_sdk_life_cycle.md`.
   - Repo Editor Worker updates `docs/architecture.md` tree section.
6. **Critique**: Critic verifies sequential lifecycle coverage, OpenAI Agents SDK alignment, and example completeness.
7. **Adjustment Loop**: If the critic finds missing lifecycle stages, orchestrator requests targeted edits and re-runs critique.
8. **Completion**: Final artifacts are accepted and packaged for pull request submission.
9. **Tracing**: The run stores decisions, revisions, and approval checkpoints for future audits.

## Outcome

This lifecycle model keeps execution modular, policy-aware, and adaptable while mapping directly to OpenAI Agents SDK concepts (agents, tools, handoffs, guardrails, sessions, and tracing).

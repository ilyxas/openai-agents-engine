# OpenAI Agents Architecture

## Core Principles

This repository provides a foundational framework for building scalable multi-agent systems based on OpenAI Agents SDK.

### Core Components:

- **Agents**: LLMs configured with instructions, tools, guardrails, and handoffs.
- **Sandbox Agents**: Agents preconfigured to work within containers, suitable for long-term and isolated tasks.
- **Agents as Tools / Handoffs**: Delegating specific tasks to sub-agents dynamically.
- **Tools**: Abstract actions enabling agents to interact with external systems (APIs, Functions, Utilities, etc.).
- **Guardrails**: Safety protocols ensuring robust input/output validation for higher stability.
- **Human-in-the-Loop (HITL)**: Mechanisms involving human intervention in workflows.
- **Sessions**: Automatic history management to maintain agent conversations coherently across runs.
- **Tracing**: Tracking agent runs for debugging and optimization.
- **Realtime Agents**: Voice agents with full `gpt-realtime-2` capabilities.

## Architectural Invariants

1. **Agent Independence**: Each agent must be modular and isolated.
2. **Tool Reusability**: Tools should allow integration across multiple workflows.
3. **Composable Flows**: Workflows should be decomposable into smaller atomic tasks.
4. **Safe Execution**: Each execution step must incorporate guardrails for validation.
5. **Tracing and Observability**: Every step must produce trace logs for monitoring and debugging.

## Repository Structure

```plaintext
openai-agents-base/
├── src/
│   ├── agents/                 # All agent definitions and implementations
│   │   ├── base_agent.py       # Abstract base agent class
│   │   ├── planner_agent.py    # Planner Agent: generates TaskGraph
│   │   ├── orchestrator.py     # Orchestrator: manages workflow execution
│   │   ├── critic_agent.py     # Observer/Critic: evaluates execution steps
│   │   ├── hitl_agent.py       # HITL (Human-in-the-Loop) agent for approvals
│   │   └── worker_agents/      # Specialized agents for atomic tasks
│   ├── core/                   # Core logic and data structures
│   │   ├── task_graph.py       # Models: TaskGraph, TaskState, TaskStep
│   │   ├── contracts.py        # Contracts defining agent input/output
│   ├── policies/               # Policies and validation rules
│   │   ├── policy_gate.py      # Validation of TaskGraph against constraints
│   ├── tracing/                # Tracing and debugging tools
│   │   ├── trace_logger.py
│   ├── flows/                  # Predefined workflows and task flows
│   │   ├── base_flow.py        # Generic execution flow
│   │   └── task_flow.py        # Example workflow
│   ├── utils/                  # Utilities and shared helpers
│   │   ├── logger.py
│   │   ├── serializers.py
├── docs/
│   ├── architecture.md         # Documentation for architecture and system design
├── tests/
│   ├── unit/                   # Unit tests
│   ├── integration/            # Integration tests
├── .github/
│   └── workflows/ci.yml        # CI/CD workflows
├── pyproject.toml              # Python project configuration
└── README.md                   # Repository overview and usage
```

## Execution Cycle

### Step-by-Step Process:

1. **Task**: The high-level intent from a user.
2. **Planner Agent**: Converts `TaskIntent` into a `TaskGraph` (a plan of steps to execute).
3. **PolicyGate**: Validates the TaskGraph according to policies (budget, safety, risks).
4. **Orchestrator**: Manages execution, delegates steps to Worker Agents, and tracks progress.
5. **Worker Agents**: Perform atomic tasks defined in TaskGraph, report results back.
6. **Observer/Critic**: Evaluates completed steps, monitors quality, and sends feedback.
7. **Human-in-the-Loop (HITL)**: Engages humans for critical decisions or approvals.
8. **Tracing**: Logs all execution details for debugging and optimization.
# EurinHash OpenCode

Architecture and execution prompt system for transforming OpenCode into the **EurinHash / HashCode Terminal Agent Command Center**.

## Objective

This repository is the source of truth for the research, architecture, UX, observability, implementation, QA and release process used to evolve the OpenCode TUI without destabilizing the underlying agent engine.

## Product architecture

```text
OpenCode Backend
      ↓
OpenCode SDK / API
      ↓
HashCode Terminal
  ├─ Command Center UI
  ├─ Agent Experience
  ├─ Observability
  ├─ Interaction / Personalization
  └─ Terminal Design System
```

## Mission-centered product model

The primary product object is the **mission**, not the chat. A mission contains its contract, tasks, resources, agents, tools, execution, validation and proof. The Command Center exposes this lifecycle without creating a second source of truth.

See `docs/EURINHASH-COMMAND-CENTER.md` and `docs/EURINHASH-MISSION-UX-FR-EN.md`.

## Prompt execution order

00. Deep Recon
01. Architecture Map
02. UX Information Architecture
03. HashCode Design System
04. State & Event Model
05. Agent Experience
06. Observability
07. Command Center UI & Layouts
08. Interaction & Personalization
09. Implementation
10. QA, Performance & Regression
11. Release, Documentation & Upstream Sync

The expanded specifications are in `prompts/MASTER-PROMPTS-DETAILED.md`.

## Governance documents

- `MASTER-PLAN.md` — product and engineering gates.
- `AGENTS.md` — mandatory coding-agent contract.
- `prompts/MASTER-PROMPTS-DETAILED.md` — detailed 12-phase execution specification.
- `docs/EXECUTION-GUIDE.md` — evidence and execution protocol.
- `docs/DELIVERABLES.md` — required artifact registry.
- `docs/TRACEABILITY-MATRIX.md` — runtime → state → UI traceability.
- `docs/ARCHITECTURE.md` — architectural constraints and invariants.
- `docs/EURINHASH-COMMAND-CENTER.md` — mission-centered Command Center contract.
- `docs/EURINHASH-MISSION-UX-FR-EN.md` — bilingual mission UX specification.

## Operating principle

Inspect the current repository before changing anything. Prefer existing OpenCode primitives, SDK boundaries and extension points. Do not invent data. Preserve working agent behavior. Separate domain state from presentation state. Every implementation phase must end with verification.

## State semantics

Keep session, request, model, stream, tool, MCP server, MCP model access, LSP, permission, workspace and UI states distinct. `UNKNOWN != ZERO`.

## Upstream reference

OpenCode upstream is actively evolving. The current upstream TUI location and the migration toward `packages/tui` / `@opencode-ai/tui` must be re-checked at execution time. The TUI/SDK boundary is therefore an explicit architectural constraint, not a fixed path assumption.

## Directory

```text
AGENTS.md
MASTER-PLAN.md
prompts/
  README.md
  MASTER-PROMPTS-DETAILED.md
  00–11 individual prompts
docs/
  ARCHITECTURE.md
  EXECUTION-GUIDE.md
  DELIVERABLES.md
  TRACEABILITY-MATRIX.md
  EURINHASH-COMMAND-CENTER.md
  EURINHASH-MISSION-UX-FR-EN.md
  recon/
  architecture/
  ux/
  design/
  state/
  agent/
  observability/
  ui/
  interaction/
  implementation/
  qa/
  release/
```

See `prompts/README.md` to begin execution.

# MASTER PROMPT 04 — STATE & EVENT MODEL

Build a rigorous state/event model for the Agent Command Center using the actual OpenCode runtime.

## Mission
Determine which states already exist, where they originate, how they propagate, and which presentation selectors are required.

## Explicitly separate
- SESSION STATE
- REQUEST STATE
- MODEL STATE
- STREAM STATE
- TOOL STATE
- MCP SERVER STATE
- MCP MODEL ACCESS STATE
- LSP STATE
- PERMISSION STATE
- WORKSPACE STATE
- GIT STATE
- UI STATE

Never collapse distinct states into one generic `status` field.

## Required event mapping
Trace events for:
- session creation/resume
- user message
- request start/end
- model selection
- streaming chunks
- tool invocation
- tool progress
- tool result
- permission request/response
- MCP connect/disconnect/error
- LSP lifecycle
- file changes
- Git changes
- errors
- cancellation
- completion

For each event document producer, payload, consumer, ordering guarantees, replay behavior and failure mode.

## Derived presentation model
Design selectors/adapters that can derive a stable UI snapshot without becoming a second source of truth.

## Deliverables
Create:
- `docs/state/domain-state.md`
- `docs/state/event-catalog.md`
- `docs/state/state-machine.md`
- `docs/state/presentation-state.md`
- `docs/state/unknown-data.md`
- `docs/state/failure-semantics.md`

Implementation may begin only after the model is internally consistent and verified against source code.

# AGENTS.md — EurinHash OpenCode

## Mission

This repository defines the architecture, prompts and engineering governance for evolving OpenCode into **HashCode Terminal / Agent Command Center** while keeping the underlying agent engine stable.

## Mandatory workflow

1. Read this file.
2. Read `prompts/MASTER-PROMPTS-DETAILED.md` and the relevant phase prompt.
3. Read all prerequisite gate artifacts.
4. Inspect the current repository, branch and upstream-sensitive paths before acting.
5. Use existing architecture, SDK contracts and extension points before introducing abstractions.
6. Separate confirmed facts from assumptions.
7. Make the smallest coherent, reviewable change.
8. Run relevant lint/typecheck/tests/build/render checks.
9. Record verification evidence, decisions and limitations.
10. Do not advance a gate without satisfying its acceptance criteria.

## Source-of-truth hierarchy

1. Current runtime/backend/API behavior.
2. Current generated SDK/API contract.
3. Existing TUI primitives and repository conventions.
4. Phase artifacts and approved architecture decisions.
5. Product/design hypotheses, which must be labeled until verified.

## Safety rules

- Never fabricate telemetry.
- Never treat unknown as zero: `UNKNOWN != ZERO`.
- Never weaken permissions or security controls to make the UI work.
- Never expose secrets through activity, logs or telemetry.
- Never silently break existing commands/keybindings.
- Never replace upstream internals merely for visual convenience.
- Never claim success without reproducible verification evidence.
- Never fabricate hidden agent reasoning or chain-of-thought.

## State semantics

Keep these domains distinct:

`SESSION · REQUEST · MODEL · STREAM · TOOL · MCP SERVER · MCP MODEL ACCESS · LSP · PERMISSION · WORKSPACE · UI`

Do not infer one state from another when an authoritative runtime source exists.

## Architecture boundary

Prefer:

`OpenCode backend → OpenCode SDK / API → HashCode TUI`

The TUI should not import backend implementation details when a stable SDK/API boundary is appropriate. If required authoritative data is missing, propose an API/SDK addition.

## UI target

```text
┌──────────────┬─────────────────────────────┬──────────────┐
│ WORKSPACE    │ CHAT / SESSION              │ AGENT        │
│ files / git  │ conversation / activity     │ state/model  │
├──────────────┴─────────────────────────────┴──────────────┤
│ ACTIVITY / EVENTS / TOOL EXECUTION                         │
├───────────────────────────────────────────────────────────┤
│ COMMAND / INPUT                                            │
└───────────────────────────────────────────────────────────┘
```

Supported presentation modes:
`MINIMAL · STANDARD · DEVELOPER · OBSERVER · DEBUG`

## Prompt order

`00 Recon → 01 Architecture → 02 UX → 03 Design System → 04 State/Event → 05 Agent → 06 Observability → 07 UI → 08 Interaction → 09 Implementation → 10 QA → 11 Release`

See `docs/EXECUTION-GUIDE.md` for evidence protocol and `docs/DELIVERABLES.md` for gate artifacts.

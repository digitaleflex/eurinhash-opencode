# HashCode Terminal — Master Prompt System

These prompts are executed by an AI coding agent against the **current** EurinHash OpenCode source tree. They define a gate-driven transformation from OpenCode TUI to the HashCode Terminal / Agent Command Center experience.

## Authoritative documents

- `prompts/MASTER-PROMPTS-DETAILED.md` — expanded master specification for all 12 phases.
- `docs/EXECUTION-GUIDE.md` — execution, evidence and failure protocol.
- `docs/DELIVERABLES.md` — artifact contract for every gate.
- `docs/TRACEABILITY-MATRIX.md` — runtime source → state → UI traceability.
- `MASTER-PLAN.md` — overall product/engineering plan.

## Sequence

| ID | Prompt | Primary output |
|---|---|---|
| 00 | Deep Recon | factual repository/runtime map |
| 01 | Architecture Map | target boundaries and ADRs |
| 02 | UX / IA | screens, states and layouts |
| 03 | Design System | terminal-native visual language |
| 04 | State & Event | canonical runtime/presentation model |
| 05 | Agent Experience | agent/tool lifecycle UX |
| 06 | Observability | truthful telemetry model |
| 07 | Command Center UI | concrete TUI composition |
| 08 | Interaction | keymaps, palette, preferences |
| 09 | Implementation | incremental engineering execution |
| 10 | QA | functional/performance/security gate |
| 11 | Release | documentation and upstream synchronization |

## Execution rule

Do not skip 00–06 simply because the desired UI looks obvious. The difficult part is mapping the UI to authoritative runtime state without duplicating OpenCode internals.

Do not start implementation before the prerequisite gates have produced their evidence.

## Global agent contract

Each prompt must:
1. inspect current code first;
2. distinguish facts from assumptions;
3. preserve existing behavior;
4. prefer existing OpenCode primitives, SDK boundaries and extension points;
5. avoid a second source of truth;
6. preserve permissions and security;
7. treat `UNKNOWN != ZERO`;
8. record verification evidence;
9. document unresolved questions and limitations.

## Canonical architecture

`OpenCode Backend → OpenCode SDK / API → HashCode TUI`

If authoritative data or an operation is missing, propose the appropriate API/SDK addition rather than importing backend implementation details into the TUI.

## Canonical state domains

`SESSION · REQUEST · MODEL · STREAM · TOOL · MCP SERVER · MCP MODEL ACCESS · LSP · PERMISSION · WORKSPACE · UI`

## Canonical agent states

`IDLE · THINKING · TOOL CALL · RESPONDING · WAITING · COMPLETED · ERROR · CANCELLED`

## Completion

A phase is complete only when its artifacts and verification evidence exist. A final release is complete only when the full chain is traceable from runtime source to UI behavior and QA evidence.

# Master Prompt System

These prompts are designed to be executed by an AI coding agent against the current EurinHash OpenCode source tree.

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

## Agent contract
Each prompt must inspect current code first, preserve existing behavior, and leave evidence of verification.

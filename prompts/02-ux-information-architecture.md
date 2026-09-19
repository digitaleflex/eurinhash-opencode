# MASTER PROMPT 02 — UX / INFORMATION ARCHITECTURE

Design the HashCode Terminal information architecture from the observed OpenCode TUI, not from an abstract mockup.

## Mission
Transform terminal telemetry into information users can understand immediately while keeping the conversation central.

## Core zones
Design and specify:
- CHAT / SESSION
- WORKSPACE
- AGENT
- TOOLS
- ACTIVITY / EVENTS
- OBSERVABILITY
- COMMAND / INPUT

## Required UX states
For every major screen and component specify:
- initial/loading
- idle
- active
- thinking
- tool call
- waiting for permission
- responding/streaming
- completed
- error
- cancelled
- unavailable
- empty
- degraded/partial data

## Layout modes
Specify behavior for:
- MINIMAL
- STANDARD
- DEVELOPER
- OBSERVER
- DEBUG

Each mode must define what is visible, hidden, collapsed and prioritized.

## Rules
1. Every number needs context.
2. Every state needs semantic meaning.
3. Every alert has a reason.
4. Do not expose telemetry merely because it exists.
5. Keep high-frequency information stable to avoid visual noise.
6. Do not let observability dominate the coding conversation.
7. Preserve keyboard-first interaction.
8. Design for narrow terminals first, then wider terminals.
9. Never create UI that depends on data the runtime cannot reliably provide.

## Deliverables
Create:
- `docs/ux/information-architecture.md`
- `docs/ux/layouts.md`
- `docs/ux/state-matrix.md`
- `docs/ux/navigation.md`
- `docs/ux/terminal-responsiveness.md`
- `docs/ux/accessibility.md`
- `docs/ux/empty-loading-error-states.md`

No implementation in this phase. End with component inventory and implementation priority.

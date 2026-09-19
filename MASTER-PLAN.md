# HASHCODE TERMINAL — MASTER PLAN

## Product target
Evolve the OpenCode terminal experience into **HashCode Terminal / Agent Command Center**: a terminal-native environment where coding conversation remains central while agent execution, tools, context, model, MCP, LSP, performance and workspace state become understandable at a glance.

## Architectural principle

Build an experience layer around the OpenCode engine rather than destabilizing or duplicating the engine:

`OpenCode Backend → OpenCode SDK / API → HashCode TUI`

The TUI owns presentation, interaction, layouts, themes, local UI preferences and presentation adapters. Backend/domain state remains authoritative in OpenCode/server/API boundaries.

## Workstreams

### A — Discovery
- repository reconnaissance
- runtime mapping
- extension-point inventory
- upstream compatibility analysis
- source-of-truth mapping

### B — Architecture
- backend/TUI/SDK boundaries
- state ownership
- event contracts
- presentation adapters/selectors
- plugin presentation isolation
- upstream migration strategy

### C — Experience
- information architecture
- terminal-native design system
- agent lifecycle
- activity center
- observability
- responsive layouts

### D — Product UI
- command center
- MINIMAL / STANDARD / DEVELOPER / OBSERVER / DEBUG modes
- command palette
- personalization
- keyboard navigation

### E — Engineering
- incremental implementation
- tests
- performance
- security
- compatibility
- bounded event-driven rendering

### F — Operations
- documentation
- release process
- changelog
- rollback
- upstream synchronization

## Gates

`RECON → ARCHITECTURE → UX → DESIGN → STATE → AGENT → OBSERVABILITY → UI → INTERACTION → IMPLEMENTATION → QA → RELEASE`

A gate is passed only when its documentation, required artifacts and verification evidence exist. If a deliverable is not applicable, record `N/A` and the reason.

## Core runtime invariants

1. `UNKNOWN != ZERO`.
2. No UI metric without a documented authoritative source or explicit unknown state.
3. Session, request, model, stream, tool, MCP server, MCP model access, LSP, permission, workspace and UI states remain distinct.
4. No second source of truth is introduced by the TUI.
5. Plugin UI failure cannot prevent base TUI startup.
6. Permissions and security boundaries are never weakened for presentation convenience.

## Core UX target

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

## Canonical observability

`SESSION · MODEL · CONTEXT · TOKENS · COST · ACTIVITY · TOOLS · PERFORMANCE · SECURITY`

Display only data supported by the runtime. Known zero cost may be `$0.00`; unknown cost is `N/A`. Known context limits may be displayed as `used / limit · percentage`; absent limits must not be invented.

## Final success condition

The result must make agent work more understandable without replacing the underlying agent engine: chat and streaming remain functional; sessions/history, providers/models, agents/tools, permissions, MCP/LSP and existing commands/keybindings remain intact; telemetry is truthful; the UI works across terminal sizes; and the complete implementation is traceable through the 12 gates.

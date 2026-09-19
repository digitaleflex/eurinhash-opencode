# MASTER PROMPT 07 — COMMAND CENTER UI / LAYOUTS

Implement the concrete terminal information architecture only after prompts 00–06 are validated.

## Target composition
```text
┌──────────────┬─────────────────────────────┬──────────────┐
│ WORKSPACE    │ CHAT / SESSION              │ AGENT        │
│ files / git  │ conversation / activity     │ state/model   │
├──────────────┴─────────────────────────────┴──────────────┤
│ ACTIVITY / EVENTS / TOOL EXECUTION                         │
├───────────────────────────────────────────────────────────┤
│ COMMAND / INPUT                                            │
└───────────────────────────────────────────────────────────┘
```

Treat this as a target concept, not a demand for these exact dimensions. Adapt to the actual OpenCode component tree and terminal constraints.

## Build requirements
- Reuse existing TUI primitives.
- Create composable components with clear ownership.
- Keep chat readable at all terminal sizes.
- Allow sidebars/panels to collapse.
- Avoid expensive full-tree rerenders.
- Preserve existing dialogs and command routing.
- Preserve mouse support where currently supported.
- Preserve keybindings and provide discoverable shortcuts.

## Layout modes
Implement configuration/state for MINIMAL, STANDARD, DEVELOPER, OBSERVER and DEBUG. Layout changes must not alter domain behavior.

## Activity center
Provide a chronological event/activity view with filtering by session, agent, tool, MCP, LSP and severity where data exists.

## Deliverables
- UI component implementation
- layout/state tests
- snapshots or equivalent terminal rendering tests where the project supports them
- `docs/ui/component-map.md`
- `docs/ui/layout-implementation.md`

Before changing existing components, document what is reused, replaced or wrapped and why.

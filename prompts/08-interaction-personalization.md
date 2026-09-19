# MASTER PROMPT 08 — INTERACTION & PERSONALIZATION

Make HashCode Terminal adaptable to different working styles without creating configuration chaos.

## Personalization domains
Design controls for:
- layout mode
- density
- sidebar visibility
- telemetry visibility
- activity verbosity
- theme
- keybindings
- notifications/attention behavior
- command aliases where supported
- persistent UI preferences

## Command center
Define a keyboard-first command palette for navigation and configuration. It must coexist with OpenCode's existing command/keymap system rather than replace it blindly.

## Interaction rules
- Commands must have predictable focus behavior.
- Escape/back behavior must remain coherent.
- Long-running operations must visibly indicate state.
- Dangerous actions require existing permission/confirmation semantics.
- User preferences must not leak into domain logic.
- Invalid configuration must fail safely and preserve usable defaults.

## Persistence
Identify existing persistence facilities first. Extend them rather than creating parallel storage without justification.

## Deliverables
Create:
- `docs/interaction/keymap.md`
- `docs/interaction/command-palette.md`
- `docs/interaction/preferences.md`
- `docs/interaction/focus-navigation.md`
- `docs/interaction/notifications.md`
- `docs/interaction/persistence.md`

Then implement only the validated pieces and add regression tests for existing commands and shortcuts.

# MASTER PROMPT 03 — HASHCODE DESIGN SYSTEM

Create the design language for HashCode Terminal as a terminal-native system, not a web UI copied into a terminal.

## Goals
Define:
- semantic colors
- typography hierarchy using terminal-safe capabilities
- spacing
- borders and separators
- icons/glyph strategy with fallbacks
- badges
- status indicators
- progress bars
- tables
- panels
- command surfaces
- alerts
- focus states
- selection states

## Semantic status vocabulary
Define visual semantics for:
- ACTIVE
- IDLE
- THINKING
- RUNNING
- WAITING
- SUCCESS
- WARNING
- ERROR
- CANCELLED
- UNKNOWN
- DISCONNECTED

Never rely on color alone. Every important state must have text/icon structure.

## Telemetry conventions
Standardize representations such as:
- `38%`
- `100K / 262K · 38%`
- `100K · 38%` when the limit is unknown
- `$0.00` when cost is known to be zero
- `N/A` when cost is unknown

## Deliverables
Create:
- `docs/design/design-tokens.md`
- `docs/design/components.md`
- `docs/design/status-language.md`
- `docs/design/iconography.md`
- `docs/design/density.md`
- `docs/design/theme-strategy.md`
- `docs/design/terminal-compatibility.md`

Reuse existing OpenCode theme primitives where appropriate. Do not hard-code styling inside business logic.

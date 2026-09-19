# EurinHash OpenCode — Architecture

## 1. Mission

Build a proprietary terminal experience around OpenCode while preserving the underlying coding-agent engine. The product target is **HashCode Terminal / Agent Command Center**: a terminal-first interface where the user can understand session, request, model, context, tools, MCP, LSP, activity, workspace and performance at a glance.

## 2. Architectural direction

```text
┌──────────────────────────────────────────────────────────────┐
│                    HASHCODE TERMINAL                         │
│  Command Center · layouts · interaction · observability      │
├──────────────────────────────────────────────────────────────┤
│                    SDK / API boundary                         │
├──────────────────────────────────────────────────────────────┤
│ OpenCode backend · sessions · messages · agents · tools       │
│ providers · models · permissions · MCP · LSP · persistence    │
└──────────────────────────────────────────────────────────────┘
```

Preferred strategy: evolve the experience layer rather than performing an uncontrolled rewrite of the agent engine.

## 3. Ownership boundaries

### Backend / server / domain
Own authoritative domain data and operations: sessions, messages, workspace/domain data, providers, models, agents, permissions, tool execution and stable API contracts.

### SDK / API
Own the stable boundary consumed by the TUI. Missing authoritative operations/data should be exposed through the API and generated SDK rather than backend imports into presentation code.

### HashCode TUI
Own presentation components, layouts, routes/dialogs, themes, keymaps, UI primitives, event consumption, tool-result presentation, presentation adapters/selectors, terminal behavior and local UI preferences.

### Plugins
Separate plugin installation/loading from plugin presentation. Optional plugin UI failures must be contained and cannot prevent base TUI startup.

## 4. Upstream constraints

The exact upstream structure must be re-checked at execution time. Relevant architectural references include the current TUI location, the TUI package extraction specification, TUI plugin specification, `@opencode-ai/sdk`, and `tui.json` / `tui.jsonc` configuration.

The expected migration direction is toward a reusable `packages/tui` / `@opencode-ai/tui` boundary. Do not hard-code an old upstream path into new architecture decisions.

## 5. Experience zones

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

## 6. Layout modes

- MINIMAL — low-noise daily mode.
- STANDARD — default command-center view.
- DEVELOPER — richer implementation telemetry.
- OBSERVER — agent/tool monitoring.
- DEBUG — dense diagnostics.

## 7. Canonical state model

Keep these states separate:

```text
SESSION STATE
REQUEST STATE
MODEL STATE
STREAM STATE
TOOL STATE
MCP SERVER STATE
MCP MODEL ACCESS STATE
LSP STATE
PERMISSION STATE
WORKSPACE STATE
UI STATE
```

Do not infer one from another when the runtime provides an authoritative source.

## 8. Canonical agent lifecycle

```text
IDLE → THINKING → TOOL CALL → RESPONDING → COMPLETED
                 ↘ WAITING
                 ↘ ERROR
                 ↘ CANCELLED
```

These are presentation states only when supported by observable runtime state. Do not fabricate hidden reasoning or claim visibility into internal chain-of-thought.

## 9. Observability model

```text
SESSION
MODEL
CONTEXT
TOKENS
COST
ACTIVITY
TOOLS
PERFORMANCE
SECURITY
```

Every metric must have documented provenance, unit, update behavior and unknown semantics.

`UNKNOWN != ZERO`.

Examples:
- known zero cost → `$0.00`;
- unknown cost → `N/A`;
- known context limit → `100K / 262K · 38%`;
- unknown context limit → `100K · 38%`.

## 10. Non-negotiable invariants

1. Chat remains functional.
2. Streaming remains functional.
3. Sessions/history remain functional.
4. Provider/model selection remains functional.
5. Agent/tool execution remains functional.
6. MCP and LSP remain functional unless explicitly changed and verified.
7. Permissions and confirmations remain safe.
8. Existing keybindings and commands are not silently broken.
9. Existing configuration remains compatible where practical.
10. No presentation component becomes a second source of truth.
11. Plugin failures cannot prevent base TUI startup.
12. Telemetry never exposes secrets or sensitive data.
13. Every implementation phase ends with tests/build/typecheck and documented evidence.

## 11. Traceability

Use `docs/TRACEABILITY-MATRIX.md` to map capabilities from runtime source → state domain → presentation. Use `docs/DELIVERABLES.md` to verify gate completeness.

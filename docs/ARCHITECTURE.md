# EurinHash OpenCode — Architecture

## 1. Mission

Build a proprietary terminal experience around OpenCode while preserving the underlying coding-agent engine. The product target is **HashCode Terminal / Agent Command Center**: a terminal-first interface where the user can understand session, request, model, context, tools, MCP, LSP, activity and performance at a glance.

## 2. Architectural direction

```text
┌──────────────────────────────────────────────────────────────┐
│                    HASHCODE TERMINAL                         │
│  Command Center UI · layouts · interaction · observability   │
├──────────────────────────────────────────────────────────────┤
│                 OpenCode TUI / SDK boundary                  │
├──────────────────────────────────────────────────────────────┤
│ OpenCode backend · sessions · messages · agents · tools       │
│ providers · models · permissions · MCP · LSP · persistence    │
└──────────────────────────────────────────────────────────────┘
```

The preferred strategy is an experience-layer evolution, not an uncontrolled rewrite of the agent engine.

## 3. Upstream constraints

Verified upstream references include:
- `packages/opencode/src/cli/cmd/tui` — current canonical TUI location in the migration period.
- `specs/tui-package.md` — TUI extraction architecture and ownership boundaries.
- `packages/opencode/specs/tui-plugins.md` — TUI plugin presentation slots and plugin contracts.
- target package `packages/tui` / `@opencode-ai/tui`.
- `@opencode-ai/sdk` as the backend boundary for the TUI.
- `tui.json` / `tui.jsonc` for TUI configuration.

The implementation agent must re-check the exact current branch because upstream changes frequently.

## 4. Experience zones

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

## 5. Layout modes

- MINIMAL — low-noise daily mode.
- STANDARD — default command-center view.
- DEVELOPER — richer implementation telemetry.
- OBSERVER — agent and tool monitoring.
- DEBUG — dense diagnostic information.

## 6. Canonical observability model

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

State semantics must remain separate:

```text
SESSION STATE
REQUEST STATE
MODEL STATE
TOOL STATE
MCP SERVER STATE
MCP MODEL ACCESS STATE
LSP STATE
STREAM STATE
```

`UNKNOWN != ZERO`. Unknown values must never be fabricated.

## 7. Non-negotiable invariants

1. Chat must remain functional.
2. Streaming must remain functional.
3. Sessions/history must remain functional.
4. Provider/model selection must remain functional.
5. Agent/tool execution must remain functional.
6. MCP and LSP integration must remain functional unless explicitly changed and verified.
7. Permissions and confirmations must remain safe.
8. Existing keybindings must not be silently broken.
9. Existing configuration must remain compatible where practical.
10. No presentation component becomes a second source of truth.
11. Plugin failures must not prevent base TUI startup.
12. Every implementation phase ends with tests/build/typecheck and a documented verification result.

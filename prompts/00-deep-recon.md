# MASTER PROMPT 00 — DEEP RECON

## Role
You are the lead reverse-engineer and software architect. You are working on the EurinHash OpenCode repository, a customization/fork intended to evolve OpenCode into HashCode Terminal / Agent Command Center.

## Mission
Before modifying code, perform a forensic repository and runtime reconnaissance. Do not implement anything in this phase.

## Instructions
1. Inspect the complete repository tree and identify package boundaries.
2. Inspect root manifests, workspace configuration, scripts, build system, tests and CI.
3. Locate the current TUI implementation and all entry points.
4. Locate SDK boundaries and server APIs consumed by the TUI.
5. Map session, message, part, agent, model, provider, tool, permission, MCP, LSP, file, Git and configuration flows.
6. Identify event/state propagation from backend to TUI.
7. Inspect existing themes, keymaps, dialogs, panels, status areas and reusable primitives.
8. Inspect TUI plugin contracts and extension points.
9. Identify configuration surfaces (`tui.json`, `tui.jsonc`, application config and environment variables).
10. Inspect persistence and local UI state.
11. Identify existing tests for TUI, state, events, SDK synchronization and commands.
12. Identify performance-sensitive rendering paths.
13. Identify accessibility and terminal compatibility constraints.
14. Identify upstream migration constraints, especially the TUI extraction toward `@opencode-ai/tui`.
15. Produce a dependency graph and data-flow graph.

## Required output
Create `docs/recon/` with:
- `repository-map.md`
- `package-map.md`
- `tui-map.md`
- `runtime-flow.md`
- `state-flow.md`
- `event-flow.md`
- `plugin-map.md`
- `configuration-map.md`
- `test-map.md`
- `risk-register.md`
- `extension-points.md`
- `open-questions.md`

## Rules
- No code changes.
- Never infer a path when the repository can be inspected.
- Quote exact file paths, symbols and responsibilities.
- Distinguish confirmed facts from hypotheses.
- Flag obsolete assumptions caused by upstream changes.
- Do not propose implementation until the reconnaissance is complete.

## Completion gate
End with a concise `RECON STATUS` containing: repository understood, TUI understood, SDK boundary understood, runtime states understood, extension points understood, unknowns remaining, recommended next prompt.

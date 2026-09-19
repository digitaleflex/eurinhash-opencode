# AGENTS.md — EurinHash OpenCode

## Mission
This repository defines the architecture, prompts and engineering governance for evolving OpenCode into HashCode Terminal / Agent Command Center.

## Mandatory workflow
1. Read this file.
2. Read the relevant master prompt.
3. Inspect the current repository before acting.
4. Use existing architecture and extension points before introducing abstractions.
5. Separate confirmed facts from assumptions.
6. Make the smallest coherent change.
7. Run relevant tests/typecheck/build.
8. Document architectural decisions and known limitations.

## Safety rules
- Never fabricate telemetry.
- Never weaken permissions or security controls to make the UI work.
- Never expose secrets through activity, logs or telemetry.
- Never silently break existing commands/keybindings.
- Never replace upstream internals merely for visual convenience.
- Do not declare success without verification.

## State semantics
Keep session, request, model, stream, tool, MCP server, MCP model access, LSP, permission, workspace and UI states distinct.

## Unknown data
`UNKNOWN != ZERO`. Use `N/A`, `UNKNOWN` or an equivalent explicit state when authoritative data is unavailable.

## Architecture boundary
Prefer:
`OpenCode backend → OpenCode SDK → HashCode TUI`

The TUI should not import backend implementation details when an SDK/API boundary is appropriate.

## Prompt order
00 Recon → 01 Architecture → 02 UX → 03 Design System → 04 State/Event → 05 Agent → 06 Observability → 07 UI → 08 Interaction → 09 Implementation → 10 QA → 11 Release.

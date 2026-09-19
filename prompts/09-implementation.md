# MASTER PROMPT 09 — IMPLEMENTATION

You are now the senior engineer responsible for implementation. Use prompts 00–08 and their generated documentation as the specification.

## Phase 0 — Revalidate
Inspect the current branch, git status, package manager, build scripts, tests and upstream-sensitive paths. Never assume the repository still matches earlier reconnaissance.

## Phase 1 — Foundation
Implement shared types, selectors/adapters and state boundaries first. Keep authoritative data in existing OpenCode state/API mechanisms.

## Phase 2 — Design system
Implement semantic theme/status primitives and reusable terminal components.

## Phase 3 — Agent experience
Implement lifecycle visualization, tool execution presentation, permission states and activity feed.

## Phase 4 — Observability
Implement context/tokens/cost/performance displays only where authoritative data exists. Handle unknown values explicitly.

## Phase 5 — Command Center
Integrate workspace, chat, agent, activity and command areas. Make layouts responsive to terminal dimensions.

## Phase 6 — Personalization
Implement layout modes, density, preferences and command palette using existing configuration/persistence patterns.

## Engineering constraints
- TypeScript strictness and repository conventions must be respected.
- Prefer existing utilities and components.
- Do not duplicate backend logic in the TUI.
- Do not introduce global mutable state unless existing architecture requires it.
- Keep rendering bounded and event-driven.
- Preserve plugin isolation and failure containment.
- Preserve security/permission semantics.
- Do not expose secrets or sensitive tool arguments in telemetry.
- Keep changes incremental and reviewable.

## Verification after each phase
Run the narrowest relevant tests first, then typecheck/build, then broader regression tests. Record commands and results.

## Completion
Update `docs/implementation/` with changed architecture, migration notes, known limitations and rollback points. Never claim completion without actual verification evidence.

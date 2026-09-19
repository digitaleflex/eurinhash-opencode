# MASTER PROMPT 01 — ARCHITECTURE MAP

Use the completed Deep Recon as evidence. Design the target architecture for HashCode Terminal without prematurely coding it.

## Objectives
- Define what remains OpenCode core.
- Define what becomes HashCode experience/presentation.
- Define server, SDK and TUI responsibilities.
- Define stable interfaces between layers.
- Define extension points for future features.

## Required analysis
Map:
- process/runtime boundaries
- package dependencies
- TUI-to-SDK calls
- event subscriptions
- state stores/signals
- rendering hierarchy
- command routing
- plugin presentation
- configuration
- persistence
- tests

For every proposed boundary specify input, output, owner, lifecycle and failure behavior.

## Architecture principles
- Dependency direction must remain intentional.
- The TUI must not reach into backend internals when an SDK/API boundary exists.
- Missing backend data must be exposed through the server API and generated SDK rather than imported directly.
- Presentation state must not duplicate authoritative domain state.
- New abstractions are justified only when they remove real coupling or enable required UX.
- Preserve upstream compatibility where practical.

## Deliverables
Create:
- `docs/architecture/target-architecture.md`
- `docs/architecture/dependency-rules.md`
- `docs/architecture/data-contracts.md`
- `docs/architecture/extension-strategy.md`
- `docs/architecture/migration-plan.md`
- `docs/architecture/adr/` with ADRs for major irreversible decisions.

## Decision format
For each major decision record: context, options, selected direction, consequences, migration cost, rollback strategy.

Do not implement. Finish with a dependency-boundary validation checklist.

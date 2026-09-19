# MASTER PROMPT 11 — RELEASE / DOCUMENTATION / UPSTREAM SYNC

Prepare HashCode Terminal for sustainable maintenance while OpenCode continues to evolve rapidly.

## Release engineering
Define:
- versioning strategy
- changelog policy
- migration notes
- compatibility policy
- feature flags if needed
- rollback strategy
- release checklist

## Documentation
Keep documentation aligned with actual implementation. Every public configuration option, layout mode, command, keybinding and telemetry field must have a clear source of truth.

## Upstream synchronization
Before every sync:
1. inspect upstream changes affecting TUI, SDK, plugins, events and APIs;
2. identify conflicts with HashCode customizations;
3. classify changes as safe, requiring adaptation, or requiring architectural review;
4. update recon/ADRs when assumptions change;
5. merge incrementally;
6. run regression tests.

Do not blindly overwrite customized TUI code with upstream changes.

## Plugin strategy
Keep presentation extension points isolated from host-side installation/loading. Plugin UI failures must be contained.

## Deliverables
Create:
- `docs/release/versioning.md`
- `docs/release/changelog-policy.md`
- `docs/release/upstream-sync.md`
- `docs/release/rollback.md`
- `docs/release/release-checklist.md`
- `CONTRIBUTING.md` if absent or update it if present
- `CHANGELOG.md` if appropriate

Finish with a maintenance model that a future contributor can follow without relying on historical chat context.

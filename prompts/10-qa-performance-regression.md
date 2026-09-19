# MASTER PROMPT 10 — QA / PERFORMANCE / REGRESSION

Audit the implemented HashCode Terminal as a production terminal application.

## Functional verification
Verify:
- startup
- session creation/resume
- chat input
- streaming
- model/provider selection
- agent switching
- tool execution
- permissions
- shell/file operations
- MCP lifecycle
- LSP lifecycle
- history/navigation
- undo/revert/fork flows where supported
- commands/keybindings
- configuration
- themes/layouts

## State verification
Exercise every documented state, including degraded and unknown-data cases. Ensure UI state never reports success while the underlying operation failed.

## Visual verification
Test narrow, medium and wide terminals. Verify clipping, wrapping, focus, scrolling, long tool names, long paths, large token values and rapid event streams.

## Performance verification
Measure:
- startup time
- first render
- event-to-render latency where measurable
- rendering under rapid streaming
- memory growth across long sessions
- behavior with large histories/activity lists

Avoid arbitrary optimization. Identify measured bottlenecks first.

## Regression strategy
Compare core OpenCode behavior before/after. Any intentional behavior change must be documented.

## Security verification
Check that logs, activity panels and telemetry do not expose credentials, API keys, environment secrets, private tool arguments or sensitive file content.

## Deliverables
Create:
- `docs/qa/test-plan.md`
- `docs/qa/regression-matrix.md`
- `docs/qa/performance.md`
- `docs/qa/security.md`
- `docs/qa/release-gate.md`

Do not mark release-ready until the release gate is fully evidenced.

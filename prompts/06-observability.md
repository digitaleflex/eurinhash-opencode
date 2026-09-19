# MASTER PROMPT 06 — OBSERVABILITY

Design a truthful, low-noise observability layer for HashCode Terminal.

## Canonical domains
Capture only data actually available from the runtime:
- SESSION: id, status, duration, startedAt
- MODEL: provider, model, limits
- CONTEXT: used, limit, percentage, status
- TOKENS: input, output, total, cache read/write when available
- COST: value, currency, known/unknown
- ACTIVITY: current phase, current tool
- TOOLS: shell, MCP, LSP and other tool classes
- PERFORMANCE: latency, duration, throughput when measurable, queue when available
- SECURITY: risk/sensitivity indicators when supported

## Truth rules
- `UNKNOWN != ZERO`.
- Never estimate a value and display it as factual.
- Never convert missing telemetry into a fake default.
- Clearly mark approximate or provider-dependent metrics.
- If a provider does not expose cost, show `N/A` rather than `$0.00`.

## UX requirements
Create compact and expanded views. Support drill-down from a summary metric to evidence. Avoid continuously changing values that cause terminal flicker.

## Performance
Prefer memoized/derived selectors, event-driven updates and bounded rendering. Do not poll aggressively if the runtime already emits events.

## Deliverables
Create:
- `docs/observability/model.md`
- `docs/observability/metrics.md`
- `docs/observability/semantics.md`
- `docs/observability/presentation.md`
- `docs/observability/performance.md`
- `docs/observability/privacy.md`

Before implementation, list every metric with its authoritative source file/symbol/API field.

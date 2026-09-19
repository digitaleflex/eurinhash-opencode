# HashCode Terminal — Deliverables Registry

This registry is the expected artifact contract for the 12 master prompts.

| Gate | Required directory | Required artifacts |
|---|---|---|
| 00 | `docs/recon/` | repository-map, package-map, tui-map, runtime-flow, state-flow, event-flow, plugin-map, configuration-map, test-map, risk-register, extension-points, open-questions |
| 01 | `docs/architecture/` | target-architecture, boundaries, data-ownership, extension-strategy, plugin-presentation, upstream-compatibility, ADRs |
| 02 | `docs/ux/` | information-architecture, screen-map, user-flows, state-ux-matrix, responsive-terminal, interaction-principles, accessibility |
| 03 | `docs/design/` | design-system, tokens, typography, components, status-language, density, themes |
| 04 | `docs/state/` | state-model, event-catalog, state-transition-matrix, selectors, unknown-data-policy, error-cancellation |
| 05 | `docs/agent/` | agent-lifecycle, tool-experience, permission-experience, long-running-operations, multi-agent-readiness, failure-recovery |
| 06 | `docs/observability/` | telemetry-model, metric-catalog, data-provenance, freshness, unknown-and-zero, security, performance-signals |
| 07 | `docs/ui/` | component-map, layout-implementation + implementation/tests |
| 08 | `docs/interaction/` | keymap, command-palette, preferences, focus-navigation, notifications, persistence |
| 09 | `docs/implementation/` | progress, verification-log, decisions, known-limitations |
| 10 | `docs/qa/` | test-plan, regression-matrix, performance, security, release-gate |
| 11 | `docs/release/` | versioning, changelog-policy, upstream-sync, rollback, release-checklist + CONTRIBUTING/CHANGELOG |

## Traceability rule

Every major implementation feature should be traceable to:
1. a runtime source discovered in Recon;
2. an architecture ownership decision;
3. a UX requirement;
4. a state/event contract;
5. an implementation/test artifact.

## Completion rule

Missing artifacts are not automatically fatal when a phase explicitly proves that a category is not applicable. In that case document `N/A`, the reason and the evidence.

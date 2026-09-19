# HashCode Terminal — Detailed Master Prompt Pack

> Authoritative execution specification for the 12-phase transformation of OpenCode into the EurinHash / HashCode Terminal Agent Command Center.
>
> **Rule:** this document expands the individual prompts. If an individual prompt and this document diverge, preserve repository facts and update both documents before implementation.

## Global agent contract

You are operating as a senior software architect, TUI engineer, product designer, observability engineer, QA engineer and release engineer as required by the current phase.

For every phase:
1. Inspect the current repository and current branch before proposing changes.
2. Read the current prompt and all prerequisite artifacts.
3. Distinguish `FACT`, `INFERENCE`, `HYPOTHESIS`, and `DECISION`.
4. Prefer existing OpenCode primitives, SDK contracts and extension points.
5. Do not duplicate backend/domain state in presentation code.
6. Never fabricate telemetry. `UNKNOWN != ZERO`.
7. Preserve permissions, confirmations, security boundaries, commands, keybindings, streaming, sessions and tool execution.
8. Make incremental, reviewable changes; avoid broad rewrites unless evidence requires them.
9. Run the narrowest useful verification after each coherent change, then the phase gate.
10. Record limitations and unresolved questions instead of silently guessing.

## Canonical architecture target

```text
OpenCode Backend
      ↓
OpenCode SDK / stable API boundary
      ↓
HashCode Terminal Experience Layer
      ├── TUI composition
      ├── semantic design system
      ├── state selectors/adapters
      ├── agent lifecycle presentation
      ├── observability
      ├── command palette / interaction
      └── local UI preferences
```

The TUI may consume authoritative data through the SDK/API. If required data or operations do not exist, propose an API/SDK addition rather than importing backend implementation details into the TUI.

## Canonical state model

Keep these distinct:
- SESSION STATE
- REQUEST STATE
- MODEL STATE
- STREAM STATE
- TOOL STATE
- MCP SERVER STATE
- MCP MODEL ACCESS STATE
- LSP STATE
- PERMISSION STATE
- WORKSPACE STATE
- UI STATE

Never infer one state from another when the runtime exposes a more authoritative source.

## Canonical observability model

```text
SESSION: id, status, startedAt, duration
MODEL: provider, model, limits, capabilities
CONTEXT: used, limit, percentage, status
TOKENS: input, output, total, cacheRead, cacheWrite
COST: value, currency, known
ACTIVITY: current, phase, tool, source
TOOLS: shell, file, MCP, LSP and execution state
PERFORMANCE: TPS, latency, requests, queue, duration
SECURITY: risk, sensitivity, permission/confirmation state
```

Display semantics:
- Known zero cost → `$0.00`
- Unknown cost → `N/A`
- Known context limit → `100K / 262K · 38%`
- Unknown context limit → `100K · 38%`
- Unknown telemetry must be visibly unknown, not guessed.

## Phase gates

```text
00 RECON
  ↓
01 ARCHITECTURE
  ↓
02 UX
  ↓
03 DESIGN
  ↓
04 STATE
  ↓
05 AGENT
  ↓
06 OBSERVABILITY
  ↓
07 UI
  ↓
08 INTERACTION
  ↓
09 IMPLEMENTATION
  ↓
10 QA
  ↓
11 RELEASE
```

A phase is complete only when its required artifacts exist and verification evidence is recorded.

---

# 00 — DEEP RECON

### Role
Lead reverse engineer and repository archaeologist.

### Mission
Build a factual map of the existing repository, runtime, TUI, SDK/API boundary, event propagation, persistence, plugin system and extension points. **Do not implement the redesign.**

### Preconditions
None. This is the first gate.

### Mandatory inspection
Inspect:
- repository tree and package boundaries;
- package managers, lockfiles, scripts and build graph;
- current TUI entry points and rendering primitives;
- session/message/part/agent/model/provider/tool/permission flows;
- MCP and LSP integration;
- event and state propagation;
- themes, keymaps, dialogs, panels, status areas and reusable components;
- TUI plugin contracts, `tui.json` / `tui.jsonc`, persistence and local UI state;
- tests, snapshots and CI;
- startup, streaming and high-frequency rendering paths;
- upstream TUI extraction/migration constraints;
- all current assumptions relevant to the proposed Command Center.

### Tasks
1. Identify authoritative sources of every proposed metric/state.
2. Trace one normal chat request from input to model request, tool execution, event stream and final response.
3. Trace session resume/history and cancellation.
4. Trace provider/model selection and capability information.
5. Trace MCP server connection and tool/model access separately.
6. Trace LSP lifecycle separately from MCP.
7. Map current UI state versus domain/runtime state.
8. Identify safe extension points and dangerous coupling.
9. Record performance-sensitive paths.
10. Identify existing behavior that must be preserved.

### Deliverables
Create `docs/recon/`:
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

### Anti-patterns
No speculative architecture, no visual implementation, no fabricated runtime facts, no backend rewrites.

### Verification
Run repository-native lint/typecheck/test/build discovery and any safe read-only diagnostics. Record exact commands and outcomes.

### Gate
Output `RECON STATUS: PASS` only if all major runtime/UI paths have a source-of-truth mapping or an explicit unresolved question.

### Handoff
01 consumes all recon artifacts.

---

# 01 — ARCHITECTURE MAP

### Role
Principal software architect.

### Mission
Convert recon evidence into a stable architecture and explicit boundaries for HashCode Terminal.

### Preconditions
00 PASS.

### Tasks
1. Define backend, SDK and TUI ownership.
2. Map domain data that must remain server/backend owned.
3. Map presentation state that may remain TUI owned.
4. Define adapters/selectors where API shape is not presentation-ready.
5. Define plugin presentation isolation.
6. Define failure containment for optional UI extensions.
7. Define upstream sync strategy around the TUI extraction.
8. Identify APIs/SDK capabilities that are missing and require proposals.
9. Write ADRs for non-obvious architectural choices.

### Required decisions
- no second source of truth;
- no TUI dependency on backend implementation internals where SDK/API is appropriate;
- plugin presentation cannot prevent base TUI startup;
- optional telemetry cannot block core chat;
- feature flags or staged rollout for risky UI changes.

### Deliverables
Create `docs/architecture/`:
- `target-architecture.md`
- `boundaries.md`
- `data-ownership.md`
- `extension-strategy.md`
- `plugin-presentation.md`
- `upstream-compatibility.md`
- `adr/` for significant decisions

### Verification
Check dependency direction, import boundaries and proposed API ownership against recon evidence.

### Gate
`ARCHITECTURE STATUS: PASS` with an explicit dependency and ownership map.

---

# 02 — UX / INFORMATION ARCHITECTURE

### Role
Senior product designer specialized in terminal UX and information architecture.

### Mission
Define how users understand and control sessions, agents, tools, context, models and workspace state without overwhelming the coding conversation.

### Preconditions
01 PASS.

### Target composition
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

### Tasks
Define:
- primary user jobs;
- screen hierarchy;
- focus model;
- information priority;
- loading, empty, degraded, error and unknown states;
- activity filtering;
- responsive behavior for narrow/medium/wide terminals;
- layout modes: MINIMAL, STANDARD, DEVELOPER, OBSERVER, DEBUG;
- navigation and keyboard behavior;
- accessibility/readability rules;
- notification rules;
- recovery paths.

### Deliverables
Create `docs/ux/`:
- `information-architecture.md`
- `screen-map.md`
- `user-flows.md`
- `state-ux-matrix.md`
- `responsive-terminal.md`
- `interaction-principles.md`
- `accessibility.md`

### Acceptance
Every major runtime state has an intentional UI treatment; no critical action depends on a hidden visual affordance.

### Gate
`UX STATUS: PASS`.

---

# 03 — HASHCODE DESIGN SYSTEM

### Role
Terminal design-system architect.

### Mission
Create a semantic visual language that makes state, hierarchy and severity legible while remaining native to terminals.

### Tasks
Define:
- semantic tokens for surface, text, muted, accent, success, warning, error, info and focus;
- typography hierarchy using terminal-safe primitives;
- spacing and density scales;
- borders, separators and panel anatomy;
- status indicators and state glyphs;
- progress indicators;
- tables, lists, badges and metric cards;
- tool-call presentation;
- code/output presentation;
- notification patterns;
- compact versus expanded density;
- theme compatibility and user customization boundaries.

### Mandatory semantic rules
Never encode meaning only through color. Pair color with text/glyph/position where practical.

### Deliverables
Create `docs/design/`:
- `design-system.md`
- `tokens.md`
- `typography.md`
- `components.md`
- `status-language.md`
- `density.md`
- `themes.md`

If implementation is appropriate only after later gates, keep this phase design-only.

### Gate
`DESIGN STATUS: PASS`.

---

# 04 — STATE & EVENT MODEL

### Role
Distributed-systems/state-model engineer.

### Mission
Define the canonical state/event semantics that allow the UI to be informative without becoming a competing runtime.

### Tasks
1. Enumerate authoritative runtime events.
2. Define normalized presentation events only where needed.
3. Map event → state transition → UI consumer.
4. Separate request lifecycle from session lifecycle.
5. Separate MCP server connectivity from MCP model access.
6. Separate tool state from agent state.
7. Define cancellation/error/retry semantics.
8. Define stale-event and out-of-order handling.
9. Define derived selectors and memoization boundaries.
10. Define unknown/null/zero semantics.

### Required agent states
`IDLE`, `THINKING`, `TOOL CALL`, `RESPONDING`, `WAITING`, `COMPLETED`, `ERROR`, `CANCELLED`.

### Deliverables
Create `docs/state/`:
- `state-model.md`
- `event-catalog.md`
- `state-transition-matrix.md`
- `selectors.md`
- `unknown-data-policy.md`
- `error-cancellation.md`

### Gate
Every UI metric/state has a documented source and transformation path.

`STATE STATUS: PASS`.

---

# 05 — AGENT EXPERIENCE

### Role
Agent UX and human-computer interaction specialist.

### Mission
Make agent execution understandable: what it is doing, why it is doing it, what it is waiting for, and what the user can do next.

### Tasks
Design presentation for:
- agent lifecycle;
- current task/phase;
- tool calls and results;
- permission requests;
- model/provider identity;
- context pressure;
- long-running operations;
- cancellation;
- errors and recovery;
- parallel/subagent activity if supported by runtime;
- handoff between user, agent and tools.

Do not invent reasoning content that the runtime does not expose. Present observable activity, not fabricated chain-of-thought.

### Deliverables
Create `docs/agent/`:
- `agent-lifecycle.md`
- `tool-experience.md`
- `permission-experience.md`
- `long-running-operations.md`
- `multi-agent-readiness.md`
- `failure-recovery.md`

### Gate
A user can distinguish agent state, request state, tool state and permission state without ambiguity.

`AGENT STATUS: PASS`.

---

# 06 — OBSERVABILITY

### Role
Observability and telemetry architect.

### Mission
Expose truthful runtime information with clear provenance, freshness and unknown semantics.

### Tasks
For every metric define:
- source;
- unit;
- precision;
- update frequency;
- lifecycle;
- availability conditions;
- unknown representation;
- whether it is authoritative or derived.

Implement or specify:
- session duration;
- model/provider;
- context usage;
- token counts;
- cache reads/writes;
- cost where available;
- latency;
- throughput/TPS where meaningful;
- tool counts and durations;
- MCP/LSP state;
- request queueing;
- security/permission status.

### Security
Never expose API keys, credentials, private environment variables, raw secrets, sensitive file content or unrestricted tool arguments in activity/telemetry.

### Deliverables
Create `docs/observability/`:
- `telemetry-model.md`
- `metric-catalog.md`
- `data-provenance.md`
- `freshness.md`
- `unknown-and-zero.md`
- `security.md`
- `performance-signals.md`

### Gate
No metric is displayed without a documented source or explicit unknown state.

`OBSERVABILITY STATUS: PASS`.

---

# 07 — COMMAND CENTER UI / LAYOUTS

### Role
Senior TUI engineer.

### Mission
Implement the concrete Command Center composition using the existing TUI architecture and the preceding contracts.

### Preconditions
00–06 PASS.

### Tasks
Implement incrementally:
1. workspace zone;
2. central chat/session zone;
3. agent/status zone;
4. activity/event center;
5. command/input zone;
6. layout mode switching;
7. collapsible panels;
8. narrow-terminal fallback;
9. bounded rendering under high-frequency streams.

Preserve existing dialogs, commands, mouse behavior, keybindings, scrolling, history and streaming.

### Required modes
- MINIMAL
- STANDARD
- DEVELOPER
- OBSERVER
- DEBUG

### Required tests
- layout state tests;
- component rendering tests;
- narrow/medium/wide terminal cases;
- rapid event stream cases;
- long path/large number/wrapping cases.

### Deliverables
- implementation;
- `docs/ui/component-map.md`;
- `docs/ui/layout-implementation.md`;
- rendering/snapshot-equivalent tests where supported.

### Gate
`UI STATUS: PASS` only after core interaction regression checks succeed.

---

# 08 — INTERACTION & PERSONALIZATION

### Role
Interaction systems engineer.

### Mission
Make the Command Center controllable, keyboard-first and persistently configurable without contaminating domain logic.

### Tasks
Implement/specify:
- command palette;
- keymap integration;
- focus navigation;
- layout/density preferences;
- sidebar visibility;
- telemetry/activity verbosity;
- theme preferences;
- notification settings;
- command aliases if supported;
- safe persistence and migration;
- reset-to-default behavior;
- dangerous-action confirmation.

Reuse the existing OpenCode TUI command/keymap/persistence primitives wherever possible.

### Deliverables
Create `docs/interaction/`:
- `keymap.md`
- `command-palette.md`
- `preferences.md`
- `focus-navigation.md`
- `notifications.md`
- `persistence.md`

### Gate
Existing commands and shortcuts continue to work, and every new preference has a safe default.

`INTERACTION STATUS: PASS`.

---

# 09 — IMPLEMENTATION

### Role
Staff-level implementation lead.

### Mission
Execute the approved design as small, verifiable engineering increments.

### Phase order
1. Foundation: types, selectors, adapters, state boundaries.
2. Design system primitives.
3. Agent experience.
4. Observability.
5. Command Center layouts.
6. Interaction/personalization.

### Rules
- TypeScript/repository conventions remain authoritative.
- No unnecessary global mutable state.
- No backend duplication.
- Event-driven rendering must be bounded and efficient.
- Optional/plugin failures are contained.
- Permissions remain unchanged unless explicitly designed and tested.
- Never place secrets in telemetry.
- Each commit-sized unit gets focused verification.

### Verification after each phase
Run applicable:
- formatter/linter;
- typecheck;
- unit/integration tests;
- TUI/render tests;
- build/package checks.

Record results in `docs/implementation/`:
- `progress.md`
- `verification-log.md`
- `decisions.md`
- `known-limitations.md`

### Gate
`IMPLEMENTATION STATUS: PASS` only when the feature set is integrated and the repository remains buildable/testable.

---

# 10 — QA / PERFORMANCE / REGRESSION

### Role
Principal QA and performance engineer.

### Mission
Prove that HashCode Terminal improves observability without breaking OpenCode behavior.

### Functional matrix
Verify:
- startup;
- new/resumed sessions;
- chat and streaming;
- provider/model selection;
- agent switching;
- tools;
- permissions;
- shell/files;
- MCP;
- LSP;
- history;
- undo/revert/fork where available;
- commands/keybindings;
- config/themes/layouts;
- errors/cancellation/retry.

### State matrix
Test normal, degraded, missing, stale, unknown and zero values for every major state/metric.

### Visual matrix
Test narrow, medium and wide terminals; wrapping, clipping, focus, scrolling, long paths, large numbers, rapid event streams and empty states.

### Performance
Measure:
- startup;
- first render;
- event-to-render latency;
- streaming stability;
- memory growth;
- large history/activity behavior;
- excessive recomputation/rerendering.

### Security
Confirm no credentials, API keys, environment secrets, sensitive file content or unsafe tool arguments leak into logs/activity/telemetry.

### Deliverables
Create `docs/qa/`:
- `test-plan.md`
- `regression-matrix.md`
- `performance.md`
- `security.md`
- `release-gate.md`

### Gate
`QA STATUS: PASS` only with reproducible evidence and no unresolved critical regression.

---

# 11 — RELEASE / DOCUMENTATION / UPSTREAM SYNC

### Role
Release engineer and upstream compatibility maintainer.

### Mission
Make the result maintainable, documented, reversible and resilient to OpenCode upstream evolution.

### Tasks
1. Define versioning and changelog policy.
2. Document migrations and compatibility assumptions.
3. Define feature flags and rollback strategy.
4. Update user/developer documentation.
5. Record exact upstream assumptions.
6. Inspect upstream changes affecting TUI, SDK, plugins, events and APIs.
7. Classify sync work as SAFE, ADAPT, or REVIEW.
8. Reconcile custom UI incrementally; never blindly overwrite it.
9. Re-run regression suite after upstream sync.
10. Update ADRs/recon documents when architecture changes.

### Deliverables
Create/update:
- `docs/release/versioning.md`
- `docs/release/changelog-policy.md`
- `docs/release/upstream-sync.md`
- `docs/release/rollback.md`
- `docs/release/release-checklist.md`
- `CONTRIBUTING.md`
- `CHANGELOG.md`

### Gate
`RELEASE STATUS: PASS` when documentation, rollback, changelog and upstream synchronization procedures are complete and verification evidence is recorded.

---

# Final acceptance criteria

The transformation is complete only when:

- the coding conversation remains central;
- agent lifecycle is understandable without fabricated internal reasoning;
- session/request/model/tool/MCP/LSP/permission states remain distinct;
- context/tokens/cost/performance telemetry is truthful;
- `UNKNOWN != ZERO` everywhere;
- workspace, activity and agent zones are usable across terminal sizes;
- command palette and keybindings coexist with existing OpenCode behavior;
- preferences persist safely;
- plugins cannot prevent base TUI operation;
- security boundaries are preserved;
- tests/typecheck/build pass for the supported target;
- release and upstream-sync procedures are documented;
- every major decision has traceable evidence from recon through implementation.

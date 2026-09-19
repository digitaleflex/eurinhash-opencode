# EURINHASH — Command Center Product & UI Contract

> Version 1.0 — 2026-09-19
> FR/EN product reference

## FR — Rôle du produit

`eurinhash-opencode` est la couche d'expérience produit et terminal. L'interface ne décide pas de la vérité métier et ne crée pas de faux états. Elle projette les états et événements fournis par le control plane/runtime.

## EN — Product role

`eurinhash-opencode` is the product and terminal experience layer. The UI does not own business truth and must not fabricate state. It projects state and events supplied by the control plane/runtime.

---

## 1. Core mental model / Modèle mental

Le **chat n'est pas l'unité de travail**. La **mission** est l'unité de travail ; le chat est une interface d'interaction.

```text
Mission
 ├── Contract
 ├── Tasks
 ├── Resources
 ├── Agents
 ├── Tools
 ├── Execution
 ├── Validation
 └── Proof
```

---

## 2. Command Center layout

```text
┌──────────────┬─────────────────────────────┬──────────────┐
│ WORKSPACE    │ CHAT / MISSION              │ AGENT        │
│              │                             │              │
│ files        │ Objective                   │ Agent        │
│ git          │ Plan                        │ Model        │
│ issue        │ Conversation                │ State        │
│ task         │ Execution                   │ Task         │
│              │ Verification                │ Tools        │
├──────────────┴─────────────────────────────┴──────────────┤
│ ACTIVITY / EVENTS / EXECUTION / EVIDENCE                  │
├───────────────────────────────────────────────────────────┤
│ COMMAND / INPUT                                           │
└───────────────────────────────────────────────────────────┘
```

### Persistent zones

- Workspace
- Chat/Mission
- Agent

### Contextual zones

- Activity
- Tasks
- Git
- MCP/LSP
- diagnostics
- evidence

### Overlay zones

- command palette
- permission confirmation
- error details
- routing explanation
- mission verification

---

## 3. Mission header

The UI should make the current mission explicit:

```text
MISSION
Implement Google OAuth

STATUS: EXECUTING
TASKS: 3/7 verified
MODEL: selected resource
ROUTING: cost-optimized
BUDGET: remaining / consumed
VERIFICATION: 4/7
RISK: current risk state
```

No metric without source, unit and meaning.

## 4. Agent panel

Display only supported runtime facts:

- identity and role;
- current state;
- current task;
- provider/model;
- context usage when available;
- permissions;
- tools;
- error/recovery state.

`CONFIGURED`, `ACTIVE`, `RUNNING` and `COMPLETED` must not be conflated.

## 5. Activity

Activity is a read-only projection of canonical events. Examples:

```text
14:32:01 Agent started
14:32:02 Context loaded
14:32:04 Model selected
14:32:04 Task T3 started
14:32:06 Command executed
14:32:12 Tests passed
14:32:12 Task T3 verified
```

The UI must never display synthetic progress as if it were runtime evidence.

## 6. Verification UX

The UI must visibly distinguish:

```text
DONE (agent claim)
      ≠
VALIDATED (technical check)
      ≠
VERIFIED (acceptance proven)
```

A verification panel should expose:

- acceptance criterion;
- status;
- evidence;
- validation command/result when applicable;
- timestamp;
- unresolved conditions.

## 7. Routing explanation

The user can inspect:

```text
WHY THIS RESOURCE?

Required capabilities
Context fit
Tool support
Health
Quota
Latency
Cost
Policy

Selected because the resource satisfies the required
threshold under the active mission constraints.
```

Rejected candidates should include a concrete reason when known.

## 8. Budgets

Mission budget UI may show:

- money;
- tokens;
- time;
- agent calls;
- risk;
- human attention.

Unknown values are displayed as unknown, never zero.

## 9. Density modes

```text
MINIMAL
STANDARD
DEVELOPER
OBSERVER
DEBUG
```

Modes change information density, not business logic or sources of truth. Narrow terminals collapse/reorder contextual panels without removing core mission/chat/input functionality.

## 10. Interaction principles

1. Keyboard-first.
2. Deterministic focus.
3. Escape always has a predictable role.
4. Interruptions are visible.
5. Errors explain cause and next action.
6. Permissions are explicit.
7. No hidden orchestration.
8. No duplicated state store.
9. No fabricated telemetry.
10. Core flows remain usable in narrow terminals.

## 11. Product boundary

The UI may request actions such as:

- inspect;
- plan;
- resolve;
- pause;
- resume;
- cancel;
- retry where authorized;
- switch view/mode;
- inspect routing;
- inspect proof.

The UI must not bypass orchestration, mutate canonical issue intent invisibly, or authorize operations that the control plane denies.

---

# EN — Product principles

The Command Center is a mission control interface, not a dashboard-first redesign. The primary object is the mission. The chat is one interaction surface inside that mission.

The UI must expose real state, explain important decisions, preserve keyboard/focus behavior, handle narrow terminals, show verification evidence, and keep permissions explicit.

The product succeeds when a user can answer at any moment:

1. What am I trying to accomplish?
2. What is the system doing now?
3. Which resources are being used?
4. Why were they selected?
5. What has actually been validated?
6. What remains unverified?
7. What evidence proves completion?

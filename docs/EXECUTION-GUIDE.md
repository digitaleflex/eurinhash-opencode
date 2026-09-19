# HashCode Terminal — Execution Guide

## Purpose

This guide defines how an AI coding agent executes the HashCode Terminal transformation without losing architectural control.

## 1. Before starting

Confirm:
- current branch and working tree state;
- package manager and lockfile;
- supported runtime/toolchain versions;
- current upstream/base revision;
- existing tests and build commands;
- all prerequisite prompt artifacts.

Do not assume the repository matches a previous audit.

## 2. Gate-driven execution

Execute strictly in this order:

`00 → 01 → 02 → 03 → 04 → 05 → 06 → 07 → 08 → 09 → 10 → 11`

Each phase must produce its artifacts before the next phase begins.

## 3. Evidence protocol

For every phase record:
- date/revision;
- commands executed;
- files inspected;
- decisions made;
- tests and their result;
- known limitations;
- unresolved questions.

Use labels:
- FACT — directly verified;
- INFERENCE — derived from verified facts;
- HYPOTHESIS — not yet verified;
- DECISION — approved design choice.

## 4. Implementation discipline

Prefer:
1. existing component/primitives;
2. existing SDK/API;
3. small presentation adapters/selectors;
4. minimal new abstractions;
5. backend/API changes only when authoritative data is genuinely missing.

Avoid:
- duplicated backend state;
- large speculative rewrites;
- UI-only workarounds that bypass permissions;
- invented metrics;
- hidden global state;
- plugin failures that crash the host TUI.

## 5. Verification loop

After each coherent implementation unit:

```text
format/lint
   ↓
typecheck
   ↓
focused tests
   ↓
render/TUI checks
   ↓
build/package check
```

Then run the broader phase gate.

## 6. Failure handling

If a phase cannot pass:
- stop progression;
- document the exact blocker;
- classify it as code, architecture, missing API, upstream change, test infrastructure or environment;
- do not bypass the gate by weakening requirements.

## 7. Upstream evolution

Re-run recon when upstream changes materially affect:
- TUI package boundaries;
- SDK contracts;
- event schemas;
- plugin contracts;
- terminal rendering primitives;
- configuration/keymap systems.

Never blindly merge upstream UI changes over custom HashCode presentation.

## 8. Final handoff

The final implementation must be explainable from:
`recon → architecture → UX → design → state → agent → observability → UI → interaction → implementation → QA → release`.

A reviewer should be able to trace every major UI decision back to a runtime source or an explicit product decision.

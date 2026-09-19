# EurinHash OpenCode

Architecture and execution prompt system for transforming OpenCode into the EurinHash / HashCode Terminal Agent Command Center.

## Objective

This repository is the source of truth for the research, architecture, UX, observability, implementation and QA prompts used to evolve the OpenCode TUI without destabilizing the underlying agent engine.

## Prompt execution order

00. Deep Recon
01. Architecture Map
02. UX Information Architecture
03. HashCode Design System
04. State & Event Model
05. Agent Experience
06. Observability
07. Command Center UI & Layouts
08. Interaction & Personalization
09. Implementation
10. QA, Performance & Regression
11. Release, Documentation & Upstream Sync

## Operating principle

Inspect the current repository before changing anything. Prefer existing OpenCode primitives, SDK boundaries and extension points. Do not invent data. Preserve working agent behavior. Separate domain state from presentation state. Every implementation phase must end with verification.

## Upstream reference

OpenCode upstream is actively evolving. The current upstream repository uses a canonical TUI under `packages/opencode/src/cli/cmd/tui` while a migration toward `packages/tui` and `@opencode-ai/tui` is specified. The TUI/SDK boundary must therefore be treated as an explicit architectural constraint.

## Directory

See `docs/ARCHITECTURE.md` for the repository map and `prompts/` for the master prompts.

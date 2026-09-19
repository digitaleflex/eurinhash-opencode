# HASHCODE TERMINAL — MASTER PLAN

## Product target
Evolve the OpenCode terminal experience into **HashCode Terminal / Agent Command Center**: a terminal-native environment where coding conversation remains central while agent execution, tools, context, model, MCP, LSP, performance and workspace state become understandable at a glance.

## Workstreams

### A — Discovery
- repository reconnaissance
- runtime mapping
- extension-point inventory
- upstream compatibility analysis

### B — Architecture
- backend/TUI/SDK boundaries
- event and state contracts
- presentation adapters
- plugin presentation model

### C — Experience
- information architecture
- terminal-native design system
- agent lifecycle
- activity center
- observability

### D — Product UI
- command center
- layout modes
- command palette
- personalization
- keyboard navigation

### E — Engineering
- incremental implementation
- tests
- performance
- security
- compatibility

### F — Operations
- documentation
- release process
- changelog
- upstream synchronization

## Gates

`RECON → ARCHITECTURE → UX → DESIGN → STATE → AGENT → OBSERVABILITY → UI → INTERACTION → IMPLEMENTATION → QA → RELEASE`

A gate is passed only when its documentation and verification evidence exist.

## Core invariant

The HashCode experience can evolve aggressively while the underlying coding-agent behavior remains stable. UI ambition must never become an excuse to duplicate or destabilize the engine.

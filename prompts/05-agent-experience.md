# MASTER PROMPT 05 — AGENT EXPERIENCE

Design the visible mental model of an AI coding agent in HashCode Terminal.

## Mission
The user must understand what the agent is doing, what it is waiting for, what it changed, and what requires attention without reading raw logs.

## Agent lifecycle
Model and visualize:
`IDLE → THINKING → TOOL CALL → WAITING → RESPONDING → COMPLETED`
with valid transitions to `ERROR` and `CANCELLED`.

Map each state to actual runtime evidence. Do not invent a state merely for animation.

## Agent panel
Specify:
- agent identity
- current model/provider
- current task/request
- current phase
- elapsed time
- active tool
- last action
- next expected action when known
- permission requirement
- error state

## Tool experience
Every tool execution should make it possible to understand:
- what tool was invoked
- why/phase when available
- arguments summary with sensitive-data protection
- progress
- duration
- result status
- failure reason

## Multi-agent readiness
Design the model so future subagents can be represented without rewriting the UI. Distinguish primary agent, subagent and tool execution.

## Deliverables
Create:
- `docs/agent/lifecycle.md`
- `docs/agent/agent-panel.md`
- `docs/agent/tool-experience.md`
- `docs/agent/permissions.md`
- `docs/agent/multi-agent.md`
- `docs/agent/error-recovery.md`

Do not implement until the runtime evidence mapping is complete.

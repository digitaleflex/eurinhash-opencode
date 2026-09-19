# HashCode Terminal — Traceability Matrix

## Product requirement → runtime → UI

| Capability | Runtime/source to verify | State domain | Presentation |
|---|---|---|---|
| Session status | session lifecycle/API/events | Session | Agent/session header |
| Request status | request/stream events | Request + Stream | Activity/status |
| Model/provider | provider/model API | Model | Agent panel |
| Context usage | authoritative context/token metadata | Model/Request | Context metric |
| Tokens | usage metadata/events | Request/Model | Token metric |
| Cost | provider usage/cost metadata | Request | Cost metric |
| Tool execution | tool call/result events | Tool | Activity center |
| MCP connectivity | MCP server lifecycle | MCP server | Tool/MCP status |
| MCP model access | model capability/access state | MCP model access | Model/MCP status |
| LSP | LSP client/server lifecycle | LSP | Workspace/status |
| Permissions | permission request/result | Permission | Confirmation UI |
| Workspace | file/git/workspace APIs | Workspace | Left panel |
| Performance | measurable event/request timings | Performance | Debug/Developer |
| Security | permission/risk metadata where available | Security | Status/confirmation |

## Required provenance

A row must not be implemented as a hard-coded metric. The implementation must document the exact source, transformation and fallback/unknown behavior.

## State separation

Do not derive:
- MCP model access from MCP server connectivity;
- request completion from session completion;
- tool completion from agent completion;
- cost from token count unless the runtime explicitly defines that calculation;
- context limit from an assumed provider default;
- security approval from tool success.

## Review questions

For every new UI value ask:
1. Who owns the data?
2. What event updates it?
3. Can it become stale?
4. What does unknown mean?
5. Is zero a valid value?
6. What happens when the provider does not expose it?
7. Could displaying it leak sensitive information?
8. Is it derived or authoritative?

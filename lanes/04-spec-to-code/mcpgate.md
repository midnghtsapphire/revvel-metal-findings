# mcpgate (maksym-mishchenko)

```json
{
  "id": "mcpgate",
  "name": "mcpgate (maksym-mishchenko)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/maksym-mishchenko/mcpgate"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "Alternative to mcp-gate for the deliver:* coder's tool boundary; same job, Go single binary. Watching because mcp-gate already holds the slot.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-09",
  "updated": "2026-10-12"
}
```

Go deny-by-default YAML MCP proxy: gates tools/call, resources/read, prompts/get, sampling; write-ahead SQLite audit (audit failure denies); `ask` parks for human approval, auto-deny on timeout; HMAC-verifiable chain export. Pushed 2026-10-07, ~2 stars.

**Revvel hit:** Alternative to mcp-gate for the deliver:* coder's tool boundary; same job, Go single binary. Watching because mcp-gate already holds the slot.

URL verified live 2026-10-09 via GitHub API.

Schema fix 2026-10-12: added the required `metal` / `determinism` scores that the 2026-10-09 entry omitted (`schema/finding.schema.json`). No asset change.

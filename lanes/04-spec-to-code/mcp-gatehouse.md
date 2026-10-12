# mcp-gatehouse

```json
{
  "id": "mcp-gatehouse",
  "name": "mcp-gatehouse",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/nickgeorgeseo/mcp-gatehouse"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Only useful if revvel-standards ships its own Python MCP server; borrow the in-server fail-closed approver pattern.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-09",
  "updated": "2026-10-12"
}
```

In-server (no proxy) permission tiers, approval gates, JSONL audit for Python MCP servers on official `mcp` SDK v1.x; gated tool with no approver fails closed. Pushed 2026-10-06, new repo.

**Revvel hit:** Only useful if revvel-standards ships its own Python MCP server; borrow the in-server fail-closed approver pattern.

URL verified live 2026-10-09 via GitHub API.

Schema fix 2026-10-12: added the required `metal` / `determinism` scores that the 2026-10-09 entry omitted (`schema/finding.schema.json`). No asset change.

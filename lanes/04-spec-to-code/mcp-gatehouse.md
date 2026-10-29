# mcp-gatehouse

```json
{
  "id": "mcp-gatehouse",
  "name": "mcp-gatehouse",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://pypi.org/project/mcp-gatehouse/",
    "https://github.com/advisories/GHSA-w4fh-qvv9-3v23",
    "https://github.com/nickgeorgeseo/mcp-gatehouse"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Only useful if revvel-standards ships its own Python MCP server; borrow the in-server fail-closed approver pattern.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-09",
  "updated": "2026-10-29"
}
```

In-server (no proxy) permission tiers, approval gates, JSONL audit for Python MCP servers on official `mcp` SDK v1.x; gated tool with no approver fails closed. Pushed 2026-10-06, new repo.

**Revvel hit:** Only useful if revvel-standards ships its own Python MCP server; borrow the in-server fail-closed approver pattern.

URL verified live 2026-10-09 via GitHub API.

Schema fix 2026-10-12: added the required `metal` / `determinism` scores that the 2026-10-09 entry omitted (`schema/finding.schema.json`). No asset change.

**Update 2026-10-29 -- MCP Python SDK advisories; set an `mcp` floor.**

- mcp-gatehouse **0.4.0** (PyPI 2026-10-21 07:49 MDT) now requires `mcp>=2,<3` (the summary above still says SDK v1.x; that is out of date).
- On 2026-10-27 (15:05–15:07 MDT) GitHub published three reviewed advisories against the MCP Python SDK, all fixed in **mcp 1.30.0 / 2.2.0**: **GHSA-w4fh-qvv9-3v23** (CVE-2026-116684, server bearer auth accepted tokens issued for another resource server; affects 1.10.0–1.29.1 and 2.0.0–2.1.1; the fix is **opt-in**: set `validate_token_resource=True` with `resource_server_url` and return the token audience from `verify_token()`), **GHSA-5h93-6whr-6q8j** (CVE-2026-116685, client transports followed cross-origin redirects with custom headers/body; from 1.8.0) and **GHSA-rwrf-2pqf-9j8j** (CVE-2026-116686, client fetched server-chosen `$ref` URLs / local files while validating tool output; from 1.10.0). Fixed versions were on PyPI since 2026-09-07; the advisories are new.
- `mcp>=2,<3` still allows 2.0.x / 2.1.x.

**Revvel hit (2026-10-29):** if revvel-standards ever ships a Python MCP server (with or without mcp-gatehouse), set **`mcp>=2.2.0`** (or `>=1.30.0` on 1.x) and do the `validate_token_resource` step; upgrading alone does not close CVE-2026-116684.

**Honesty (2026-10-29):** CAN-PARTIAL. Verified 2026-10-29 (America/Denver): GitHub advisories API (ranges, fixed versions, publish times) and advisory pages 200; PyPI JSON for mcp-gatehouse 0.4.0 `requires_dist` and mcp 1.30.0 / 2.2.0 upload times; migration detail from the al-ice.ai write-up (2026-10-28), cross-checked against the advisory summary. Not trialled.

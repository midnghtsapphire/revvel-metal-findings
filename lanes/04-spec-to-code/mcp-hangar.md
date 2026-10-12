# mcp-hangar

```json
{
  "id": "mcp-hangar",
  "name": "MCP Hangar",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/mcp-hangar/mcp-hangar",
    "https://pypi.org/project/mcp-hangar/",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.26.0"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Runtime twin of agentgate's lock: tool-schema digest pinning fails the coder's call closed when an upstream rewrites a tool description; `mcp-hangar pin --check` exits 1 in CI. Watching because it is a full fleet enforcement plane (Python, RBAC/OIDC, SIEM) and mcp-gate already holds the proxy slot.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12"
}
```

**MCP Hangar** -- self-hosted MCP policy enforcement plane in Python. Deterministic L7 admission/egress policy (which upstream, which tool, which arguments; no anomaly scores or learned baselines, so every verdict is reproducible from the policy), **tool-schema digest pinning** (`mcp-hangar pin --write` records a digest per tool; a changed description or schema is refused with `Tool '<name>' schema does not match its pinned digest`; `pin --check` prints both digests and exits 1), per-tenant tool projection that fails closed on unknown identity, API-key/OIDC identity with RFC 8707 audience binding, attributable audit with SIEM export. Over stdio the spawning process is the declared principal; over HTTP it refuses a non-loopback bind without auth. PyPI **2.26.0** (uploaded 2026-10-12 05:56 MDT; first upload 2026-01-12); release `v2.26.0` → `e6e1d6b9e2c510da8c63c1598a682be1a745a80a`; MIT; ~18★; OpenSSF Best Practices badge; listed in the official MCP registry as `io.mcp-hangar/hangar`.

**Revvel hit:** borrow the idea, not the stack: the digest-pin check is the runtime half of **agentgate**'s CI lock. Only worth running if revvel-standards ends up fronting several MCP servers for the coder; otherwise **mcp-gate** (policy) + **agentgate** (lock) cover it with less to operate.

**Honesty:** CAN-PARTIAL. Verified 2026-10-12 (America/Denver): repo live (MIT, not archived, pushed 2026-10-12), PyPI 2.26.0 live, release page 200. The 2.0 line changed approval delivery (Slack adapter you run yourself) and approval authorization; 1.6.x is closed. Heavy for a single-repo pipeline.

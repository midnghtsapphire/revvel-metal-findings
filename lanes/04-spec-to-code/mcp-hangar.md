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
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.28.0"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Runtime twin of agentgate's lock: tool-schema digest pinning fails the coder's call closed when an upstream rewrites a tool description; `mcp-hangar pin --check` exits 1 in CI; since 2.28.0 pins bind to the upstream identity and new tools can be withheld until pinned. Watching because it is a full fleet enforcement plane (Python, RBAC/OIDC, SIEM) and mcp-gate already holds the proxy slot.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12"
}
```

**MCP Hangar** -- self-hosted MCP policy enforcement plane in Python. Deterministic L7 admission/egress policy (which upstream, which tool, which arguments; no anomaly scores or learned baselines, so every verdict is reproducible from the policy), **tool-schema digest pinning** (`mcp-hangar pin --write` records a digest per tool; a changed description or schema is refused with `Tool '<name>' schema does not match its pinned digest`; `pin --check` prints both digests and exits 1), per-tenant tool projection that fails closed on unknown identity, API-key/OIDC identity with RFC 8707 audience binding, attributable audit with SIEM export. Over stdio the spawning process is the declared principal; over HTTP it refuses a non-loopback bind without auth. PyPI **2.28.0** (uploaded 2026-10-16 00:22 MDT; first upload 2026-01-12); release `v2.28.0` published 2026-10-16 00:02 MDT; MIT; OpenSSF Best Practices badge; listed in the official MCP registry as `io.mcp-hangar/hangar`.

**2.26.0 → 2.27.5 (2026-10-13…14):** `ssrf.trusted_networks` for registered remote endpoints (2.27.0); discovery health-check fallback via MCP `initialize` (2.27.1); approval resolve/expire/cancel race fixes with row-count checks (2.27.4 security); fail-closed boot/reload on unreadable access-policy keys + corrected README allow/deny spelling (2.27.4); `Mcp-Param-*` vs body compare restored under mcp SDK 2.3.0 path (2.27.4); mcp/mcp-types pin moved 2.0.0 → 2.3.0 with documented exactness (2.27.5); `init` writes absolute launcher + XDG state paths (2.27.5). Still watching — fleet plane, not the default proxy.

**2.27.5 → 2.28.0 (2026-10-16):** digest pins can be **bound to the upstream** they were taken from (`tool_projection.upstream`: remote origin, container image, or executable + command-line hash; never the server id or a secret), so a pin block copied to another server or a renamed server pointed elsewhere is refused under `block` and `pin --check` reports `(upstream)` drift (#1881); `tool_projection.new_tools: withhold` hides a tool that appears after pinning until it is pinned, emitting one `ToolAdmissionRequested` event with the definition digest (#1882); pins now have an append-only history in the event log (`ToolPinRecorded` / `ToolPinRevoked`, approver recorded as `config`) and `mcp-hangar why --tool NAME` prints it read-only (#1883); `mcp-hangar why` lists recent refusals with expected/observed digests from the SQLite store, read-only (#1871); `serve --http` now binds `127.0.0.1` by default (#1831); built-in least-privilege `kubernetes-operator` role (#1878); `init --undo` restores client configs byte-for-byte (#1870); plus ~25 fixes (graceful reload actually drains, subprocess `args` passed through, `hangar_approve` works on pending servers, metrics read real counters). Still watching.

**Revvel hit:** borrow the idea, not the stack: the digest-pin check is the runtime half of **agentgate**'s CI lock. New in 2.28.0 and worth copying as a pattern: bind each pin to the upstream it came from, and withhold (not just warn on) a tool the coder has never seen until a human pins it. Only worth running if revvel-standards ends up fronting several MCP servers for the coder; otherwise **mcp-gate** (policy) + **agentgate** (lock) cover it with less to operate.

**Honesty:** CAN-PARTIAL. Verified 2026-10-16 (America/Denver): PyPI 2.28.0 JSON (MIT), release v2.28.0 via GitHub API, `CHANGELOG.md` on `main` read for the 2.28.0 section. Earlier: repo live (MIT, not archived) 2026-10-14. The 2.0 line changed approval delivery (Slack adapter you run yourself) and approval authorization; 1.6.x is closed. Heavy for a single-repo pipeline.

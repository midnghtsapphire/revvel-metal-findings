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
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.28.0",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.30.0",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.31.0"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Runtime twin of agentgate's lock: tool-schema digest pinning fails the coder's call closed when an upstream rewrites a tool description; `mcp-hangar pin --check` exits 1 in CI; pins bind to the upstream identity (2.28.0), and since 2.30.0 a drifted tool under a `block` pin is withheld from `tools/list` (not just refused on call) and a pinned tool is served with only the pinned fields (name, description, inputSchema, outputSchema), so `title`/`_meta`/`annotations` cannot smuggle instructions or a fake readOnlyHint. Watching because it is a full fleet enforcement plane (Python, RBAC/OIDC, SIEM) and mcp-gate already holds the proxy slot.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12",
  "updated": "2026-10-20"
}
```

**MCP Hangar** -- self-hosted MCP policy enforcement plane in Python. Deterministic L7 admission/egress policy (which upstream, which tool, which arguments; no anomaly scores or learned baselines, so every verdict is reproducible from the policy), **tool-schema digest pinning** (`mcp-hangar pin --write` records a digest per tool; a changed description or schema is refused with `Tool '<name>' schema does not match its pinned digest`; `pin --check` prints both digests and exits 1), per-tenant tool projection that fails closed on unknown identity, API-key/OIDC identity with RFC 8707 audience binding, attributable audit with SIEM export. Over stdio the spawning process is the declared principal; over HTTP it refuses a non-loopback bind without auth. PyPI **2.28.0** (uploaded 2026-10-16 00:22 MDT; first upload 2026-01-12); release `v2.28.0` published 2026-10-16 00:02 MDT; MIT; OpenSSF Best Practices badge; listed in the official MCP registry as `io.mcp-hangar/hangar`.

**2.26.0 → 2.27.5 (2026-10-13…14):** `ssrf.trusted_networks` for registered remote endpoints (2.27.0); discovery health-check fallback via MCP `initialize` (2.27.1); approval resolve/expire/cancel race fixes with row-count checks (2.27.4 security); fail-closed boot/reload on unreadable access-policy keys + corrected README allow/deny spelling (2.27.4); `Mcp-Param-*` vs body compare restored under mcp SDK 2.3.0 path (2.27.4); mcp/mcp-types pin moved 2.0.0 → 2.3.0 with documented exactness (2.27.5); `init` writes absolute launcher + XDG state paths (2.27.5). Still watching — fleet plane, not the default proxy.

**2.27.5 → 2.28.0 (2026-10-16):** digest pins can be **bound to the upstream** they were taken from (`tool_projection.upstream`: remote origin, container image, or executable + command-line hash; never the server id or a secret), so a pin block copied to another server or a renamed server pointed elsewhere is refused under `block` and `pin --check` reports `(upstream)` drift (#1881); `tool_projection.new_tools: withhold` hides a tool that appears after pinning until it is pinned, emitting one `ToolAdmissionRequested` event with the definition digest (#1882); pins now have an append-only history in the event log (`ToolPinRecorded` / `ToolPinRevoked`, approver recorded as `config`) and `mcp-hangar why --tool NAME` prints it read-only (#1883); `mcp-hangar why` lists recent refusals with expected/observed digests from the SQLite store, read-only (#1871); `serve --http` now binds `127.0.0.1` by default (#1831); built-in least-privilege `kubernetes-operator` role (#1878); `init --undo` restores client configs byte-for-byte (#1870); plus ~25 fixes (graceful reload actually drains, subprocess `args` passed through, `hangar_approve` works on pending servers, metrics read real counters). Still watching.

**Revvel hit:** borrow the idea, not the stack: the digest-pin check is the runtime half of **agentgate**'s CI lock. New in 2.28.0 and worth copying as a pattern: bind each pin to the upstream it came from, and withhold (not just warn on) a tool the coder has never seen until a human pins it. Only worth running if revvel-standards ends up fronting several MCP servers for the coder; otherwise **mcp-gate** (policy) + **agentgate** (lock) cover it with less to operate.

**Honesty:** CAN-PARTIAL. Verified 2026-10-16 (America/Denver): PyPI 2.28.0 JSON (MIT), release v2.28.0 via GitHub API, `CHANGELOG.md` on `main` read for the 2.28.0 section. Earlier: repo live (MIT, not archived) 2026-10-14. The 2.0 line changed approval delivery (Slack adapter you run yourself) and approval authorization; 1.6.x is closed. Heavy for a single-repo pipeline.

**2.28.0 → 2.30.0 (2026-10-17…19):**

- **2.29.0** (release 2026-10-17 03:16 MDT): pin history over REST (`GET /api/admin/tools/pins`, `audit:read`), CEF signatures for `ToolPinRecorded`/`ToolPinRevoked` (#1886); `config check` now runs the same checks as boot/reload, so a file the gateway would refuse fails the check (#1888); a call refused by an enforced L7 egress policy no longer cold-starts the target server first (#1889); `hangar_call(max_attempts=1)` now means exactly one attempt (#1895); `oidc.clock_skew_leeway_seconds` actually read (#1891); `/api/config/diff` and `/backup` no longer take a `config_path` (arbitrary-file read) (#1892). Security: fleet-wide tool withdraw/restore needs the admin grant (#1894); `mcp-hangar add` no longer writes prompted secrets into `config.yaml`, created config files are 0600 (#1893).
- **2.29.1** (release 2026-10-18 14:32 MDT): upstream `isError: true` results pass through whole (`_meta`, `structuredContent`) (#1915); governance extensions renamed to SEP-2133 ids `io.mcp-hangar/digest-pinning` etc., dotted forms deprecated for one minor (#1914); a non-mapping `tool_projection` or a bad `digest_enforcement` value now **refuses the config** instead of silently running the default mode (#1909); failed `hangar_*` tools answer `isError: true` (#1911).
- **2.30.0** (release 2026-10-19 06:49 MDT; PyPI 07:10 MDT): **a tool that drifted from its `block`-mode digest pin is withheld from every listing the model reads** (front-door `tools/list` on stdio and streamable HTTP, `hangar_tools`), its call answered as a nonexistent tool, `notifications/tools/list_changed` on withhold/return (#1920) -- before this, the call was refused but the rug-pulled description still reached the model on every listing; **pinned tools are served with only the four pinned fields** (`name`, `description`, `inputSchema`, `outputSchema`) through one shared allow-list, so an upstream cannot keep the digest and add instructions in `title`/`_meta` or add `annotations: {readOnlyHint: true}` to skip a client confirmation; digest unchanged, existing pins stay valid; registry hot-loaded servers get secrets only from an operator allowlist (`hot_loading.secrets.allow`), a fixed base environment, `trusted_namespaces` verification, and `force_unverified` ignored unless the operator allows it. Release assets include an in-toto `mcp-hangar.intoto.jsonl`.

**Revvel hit (2026-10-19):** two more patterns worth copying into whatever fronts the coder's MCP tools (mcp-gate + agentgate today): (1) a drifted tool must disappear from the listing, not only fail on call, because the listing is model input; (2) a pinned tool should be re-served with only the fields the pin covers. Still watching (fleet plane).

**Honesty (2026-10-19):** CAN-PARTIAL. Verified 2026-10-19 (America/Denver): PyPI JSON 2.30.0 (MIT; release history 2.29.0 / 2.29.1 / 2.30.0), GitHub releases API bodies for v2.29.0, v2.29.1, v2.30.0 read in full, release page v2.30.0 200. Three releases in three days; pin exact versions if trialled.

**Update 2026-10-20 -- 2.31.0** (release 2026-10-19 11:12 MDT; PyPI 11:33 MDT): **`mcp-hangar approvals list|approve|deny`** resolves a call held on an `approval_list` by a gateway that runs over **stdio** (no REST API), through the same resolution chokepoint as `POST /api/approvals/{id}/resolve`, so expiry, compare-and-swap and tenant scoping are unchanged; the waiting gateway sees the decision on its next store poll (~2 s). The approver is always the declared `auth.stdio.principal` (a config without one is refused) and must hold `approval:resolve` even with auth off (`viewer` refused). Before this, a held stdio call could only time out. Also `hangar_whoami` (caller's principal / tenant / roles, refused for anonymous callers), dead `PolicyPushRejected` event removed, env parsing fixes for the legacy `python -m mcp_hangar.server` entry point (#1712), and mutation events recorded only when a mutator applies (#1574).

**Revvel hit (2026-10-20):** a local stdio coder host can now park a tool call for a human decision from a second terminal without opening an HTTP surface -- the same "held call, human resolves, timeout = deny" shape the deliver:* approval record wants. Still watching (fleet plane; pattern reference only).

**Honesty (2026-10-20):** CAN-PARTIAL. Verified 2026-10-20 (America/Denver): PyPI JSON 2.31.0 (MIT), GitHub release v2.31.0 body read in full, release page 200. Pin exact versions if trialled; releases are frequent.

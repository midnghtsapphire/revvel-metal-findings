# mcp-hangar

```json
{
  "id": "mcp-hangar",
  "name": "MCP Hangar",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.34.6",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.34.7",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.34.5",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.34.4",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.34.3",
    "https://github.com/mcp-hangar/mcp-hangar",
    "https://pypi.org/project/mcp-hangar/",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.28.0",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.30.0",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.31.0",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.32.0",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.32.1",
    "https://github.com/mcp-hangar/mcp-hangar/releases/tag/v2.34.8",
    "https://pypi.org/project/mcp-hangar/2.34.8/"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Runtime twin of agentgate's lock: tool-schema digest pinning fails the coder's call closed when an upstream rewrites a tool description; `mcp-hangar pin --check` exits 1 in CI; pinned tools are served with only pinned fields. 2.34.2 fixes several silent pin bypasses (unreadable/uppercase/`sha256:`-prefixed digest pins dropped, `new_tools: withhold` letting the first call through, `pin --check` misreporting drift under `mode: group`, `add` dropping pins). 2.34.4 lets a discovery approval bind to the definition's full SHA-256 `definition_digest` (a changed definition is refused, 409) and fixes an HTTP-gateway hang; 2.34.5 makes a refused/failed approval answer approved:false and keep the change pending (it used to answer approved:true and drop it). If trialled, pin ==2.34.5 (==2.34.3 still acceptable; floor >=2.34.2). Watching because it is a full fleet enforcement plane (Python, RBAC/OIDC, SIEM) and mcp-gate already holds the proxy slot.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12",
  "updated": "2026-10-30"
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

**Update 2026-10-21 -- 2.32.0 / 2.32.1.** **2.32.0** (release 2026-10-20 11:43 MDT; PyPI 12:05 MDT): `GET /api/mcp_servers/{id}` and `hangar_details` report `provenance` (`human` vs `discovery`); a key-pinned server's `key_ref` can be changed (`PUT`) and a deleted key-pinned server's name forgotten (`DELETE .../peer_identity`), both needing `mcp_servers:peer_identity` (ADR-030 §7, §9); config updates reach every replica without restart. **2.32.1** (release 2026-10-21 03:04 MDT; PyPI 03:26 MDT) is a fix release for **mixed-version fleets**: built-in roles are now enforced as the running release defines them (an older replica could strip or restore permissions on a shared auth store, and a custom role can no longer take a built-in name, #1994); a database trigger refuses a configuration row under a recorded key-pinned name unless it carries the recorded `key_ref`, so a 2.31.0-or-older replica cannot rewrite a key-pinned server as a plain one during a rolling upgrade (#1995); a forget/re-create race on the peer-key name record is closed.

**Revvel hit (2026-10-21):** one more pattern: when a gate's rules live in a shared store, enforce the rules of the running binary and refuse writes an older binary could make (DB-level trigger), rather than trusting whichever replica wrote last. Single-host revvel use is unaffected. If trialled, skip 2.32.0 and pin `==2.32.1`. Still watching.

**Honesty (2026-10-21):** CAN-PARTIAL. Verified 2026-10-21 (America/Denver): PyPI JSON (2.32.0 and 2.32.1 upload times, MIT), GitHub releases API bodies for v2.32.0 and v2.32.1 read (first ~1.8k chars each).

**Update 2026-10-22 -- 2.33.0** (GitHub release 2026-10-21 14:45 MDT; PyPI 15:07 MDT). One addition (#1998): a key-pinned server may declare where its keys come from, `tls.peer_identity.issuance: kbs-attested` (ADR-030 §2), from a closed set; anything else is refused at load. Calls record it as `declared_key_issuance` on `ToolInvocationCompleted` / `ToolInvocationFailed`, carried in JSON-lines, LEEF, syslog and OTLP exports (not CEF). Hangar records the declaration and does **not** verify it; it changes neither the pin digest nor the accepted keys.

**Revvel hit (2026-10-22):** none new for single-host revvel; a recorded-but-unverified claim is not a gate. If trialled, `==2.33.0` is safe to take over 2.32.1 (no fix content), but nothing requires it. Still watching.

**Honesty (2026-10-22):** CAN-PARTIAL. Verified 2026-10-22 (America/Denver): GitHub release v2.33.0 body read (API), PyPI JSON 2.33.0.

**Update 2026-10-26 -- 2.34.0 → 2.34.3 (security; re-pin).** PyPI and GitHub releases, all MIT:

- **2.34.0** (2026-10-23 08:35 MDT): `mcp-hangar init` moves the MCP servers Claude Code / Cursor already list behind Hangar (starts each once, pins every tool, `init --undo` restores). Front-door `tools/list` etc. now decide each name on the member a call would actually route to (#2022). `pin` now starts the server with its configured args (pins were previously taken from a differently started process). Security: opentelemetry floor 1.45.1 (CVE-2026-114603); SSRF guard refuses `fc00::/7` and `100.64.0.0/10`.
- **2.34.1** (2026-10-24 00:16 MDT): `hangar_tools` / `hangar_details` decide through `decide()` and hide withdrawn tools.
- **2.34.2** (2026-10-25 08:22 MDT), many security fixes, including: digest pins that were unreadable, uppercase or `sha256:`-prefixed were **silently dropped, leaving tools unpinned** (#2039); `new_tools: withhold` let the first call through (#2035); `pin --check` broke on `mode: group` (exit 2, drift misreported) (#2063); `mcp-hangar add` silently replaced servers and dropped pins (#2043); `local_launch` permission now required (a developer role could run code on the host) (#2026); config API leaked secrets (#2030); OIDC issuer tenant binding (#2045); k8s/docker discovery could choose commands or mounts (#2038); `opa.require_both` (#2082); removed role_assignments now revoked (#2053); compose files bind loopback (#2041).
- **2.34.3** (2026-10-25 12:02 MDT): `why` CLI event-store path fix only.

**Revvel hit (2026-10-26):** the lesson for any revvel pin check: a malformed pin must fail closed, never be skipped, and a "withhold new tools" policy must hold the first call too. If trialled, move the pin from `==2.32.1` to **`==2.34.3`** (do not run anything below 2.34.2). Still watching.

**Honesty (2026-10-26):** CAN-PARTIAL. Verified 2026-10-26 (America/Denver): GitHub releases API bodies v2.34.0–v2.34.3, PyPI JSON upload times. Not trialled.

**Update 2026-10-27 -- 2.34.4 / 2.34.5.** MIT, no security label on either release.

- **2.34.4** (GitHub release 2026-10-26 09:46 MDT; PyPI 10:09 MDT): a discovery approval can now be bound to the discovered definition's full SHA-256 `definition_digest`; if the definition changed between review and approval, the approval is refused with `DiscoveredDefinitionChangedError` (HTTP 409), and an unbound approval is logged as `discovery_approval_not_bound` (#2126). A client that disconnects mid-request on legacy `POST /mcp` with `Mcp-Method` / `Mcp-Name` headers no longer hangs the whole HTTP gateway (#2124). Fleet fixes: a deleted server leaves its groups (a group used to restart it outside the fleet, #2117); a discovered server no longer comes back as static after restart (#2110); discovery no longer deletes an operator-defined server (#2115); front-door warm-up/shutdown fixes. `McpServerFailoverSaga` sagas deprecated.
- **2.34.5** (GitHub release 2026-10-27 04:02 MDT; PyPI 04:25 MDT): a refused or failed approval now answers `approved: false` and keeps the change in quarantine / pending; before, it answered `approved: true` and dropped the entry (#2137, #2142).

**Revvel hit (2026-10-27):** two more patterns for the spec-approved / deliver:* approval check: bind an approval to the full digest of the exact thing reviewed and refuse on mismatch, and make a refused or errored approval report *not approved* while keeping the item pending, never "approved" by default. If trialled, move to **`==2.34.5`**; `==2.34.3` stays acceptable; never below 2.34.2. Still watching.

**Honesty (2026-10-27):** CAN-PARTIAL. Verified 2026-10-27 (America/Denver): GitHub releases API bodies v2.34.4 and v2.34.5, release pages 200, PyPI JSON upload times. Not trialled.

**Update 2026-10-29 -- 2.34.6 (not on PyPI) and 2.34.7 (security floor for the `full` extra).**

- **v2.34.6** (GitHub release 2026-10-29 01:10 MDT) was **never published to PyPI**: its release job failed on a pytest 9.2 incompatibility (#2146). Its fix: refusing a change to a discovered server that was since deleted no longer leaves anything tracked (#2144, closes #2143).
- **v2.34.7** (GitHub release 2026-10-29 02:00 MDT; PyPI 02:23 MDT) carries the 2.34.6 changes, caps pytest below 9.2 in the dev extra (#2147), and is a **security fix for the `full` extra**: it now requires `fpdf2>=2.8.8` (CVE-2026-114609, CVE-2026-114610; #2150). The old floor (`>=2.8.0`) let an install keep a vulnerable fpdf2; the project lockfile already resolved 2.8.9.
- Dependency check: 2.34.7 pins `mcp==2.3.0` / `mcp-types==2.3.0`, which is above the MCP Python SDK fix line (2.2.0) for the three advisories published 2026-10-27 (GHSA-w4fh-qvv9-3v23, GHSA-5h93-6whr-6q8j, GHSA-rwrf-2pqf-9j8j).

**Revvel hit (2026-10-29):** no new pattern; this is a pin bump. If trialled, move to **`==2.34.7`** (required if the `full` extra is used, otherwise make sure `fpdf2>=2.8.8`); `==2.34.5` stays acceptable without `full`; never below 2.34.2; there is no 2.34.6 on PyPI, so don't pin it.

**Honesty (2026-10-29):** CAN-PARTIAL. Verified 2026-10-29 (America/Denver): GitHub releases API bodies v2.34.6 and v2.34.7, release pages 200, PyPI JSON (2.34.7 upload time, `requires_dist`). CVE details not read beyond the release note. Not trialled.

**Update 2026-10-30 -- 2.34.8 (security/privacy):** GitHub release **v2.34.8** 2026-10-30 05:19 MDT, PyPI 05:43 MDT. Fixes a tenant data leak in the group views: `hangar_details` showed every member of a group to every tenant (#2154), and `hangar_list`, `hangar_group_list`, `GET /api/groups` and `GET /api/groups/{id}` did the same (#2158). A tenant-bound caller now sees only the members it can route to. `requires_dist` unchanged (`mcp==2.3.0`, `mcp-types==2.3.0`, `fpdf2>=2.8.8` for `full`).

**Revvel hit (2026-10-30):** pin bump only. If trialled, **`==2.34.8`**; it matters most when more than one tenant shares a hangar with auth on. `==2.34.7` stays acceptable for a single-tenant / auth-off trial. Still never below 2.34.2, and 2.34.6 does not exist on PyPI. See **mcp-digest-vectors** (02) for a known-answer set to run the digest pin against.

**Honesty (2026-10-30):** CAN-PARTIAL. Verified 2026-10-30 (America/Denver): GitHub releases API body for v2.34.8, release page and PRs #2154 / #2158 pages 200, PyPI JSON (2.34.8 upload time and `requires_dist`). Not trialled.

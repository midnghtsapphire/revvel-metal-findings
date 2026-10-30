# agentgate

```json
{
  "id": "agentgate",
  "name": "AgentGate (mcp-agentgate)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/wookat/agentgate",
    "https://www.npmjs.com/package/mcp-agentgate",
    "https://github.com/wookat/agentgate/releases/tag/v0.67.61",
    "https://agentgate.zalize.com"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* — commit `agentgate.lock` (exact MCP tool names, descriptions, input schemas the coder sees); `npx mcp-agentgate ci` exits 1 on any drift, so a server that rewrites a tool under the coder turns the deliver:* check red; `deps` flags hallucinated/typosquatted npm+PyPI packages a coder PR adds",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12",
  "updated": "2026-10-30"
}
```

**AgentGate** -- supply-chain gate for MCP servers, Node ≥ 22, npm package **`mcp-agentgate`** (command `agentgate`). Five verbs: `scan` (12 deterministic static rules: tool poisoning/hidden Unicode, credential leaks, SSRF/RCE vectors, over-privileged tool combos; live probing is opt-in `--live` and asks first), `lock` (pins the exact tool surface — names, descriptions, input schemas, optionally skill/instruction files with `--skills` — into `agentgate.lock`), `ci` / `diff` (fail on any drift from the lock, with a readable JSON diff: `tool-added`, `description-changed`, `schema-changed`, …), `deps` (live npm/PyPI check of manifests *and* source imports for slopsquatted/typosquatted names), and `advisory check` against a public MCP advisory feed. Frozen CLI contract (`docs/spec/cli-contract.md`): exit 0 clean, 1 gate failure (drift, findings at/above `--fail-on`, or `lock` could not capture a surface), 2 usage/env error (missing or invalid lockfile, unparseable explicit config). Works offline, no account or token. Ships a GitHub Action (`wookat/agentgate/packages/action@v0.67.61`) with per-finding annotations and SARIF upload, plus a pre-commit hook. npm **0.67.61** (published 2026-08-16; first publish 2026-08-04; 102 versions); tag `v0.67.61` → `fbce290fd0de6d86977f1b7d100170848d5ed32c`; main tip `67b83452265fa4870ebc3beb876d84c30a115975` (2026-09-07); Apache-2.0 LICENSE.

**Revvel hit:** fills the one gap the runtime MCP gates (**mcp-gate**, **verax**, **mcpgate**) leave open: they check *calls* against a policy, but not whether the tool *definition* the coder was approved to use is still the one being served. Commit `agentgate.lock` next to the coder's MCP config and add `agentgate ci` as a required step beside existing `deliver:*` CI; a re-approved lock is the human act, an unexplained diff is a red check. `deps --fail-on high` on coder PRs catches invented package names before install. Same pipeline, one more check; not a second pipeline.

**Honesty:** CAN-PARTIAL. Verified 2026-10-12 (America/Denver): repo live (Apache-2.0, not archived), npm registry 0.67.61 live (npmjs.com web page bot-blocks the fetcher with 403; registry JSON is the receipt), release tag and docs site 200, CLI contract read from the repo. Single maintainer, 0★, very high version churn (102 publishes in ~2 weeks of August, quiet since) — pin the exact version. Advisory feed and website are run by the maintainer; keep the gate to `lock`/`ci`/`deps` so it stays offline and deterministic. Lockfile pinning is a crowded niche (nkwib/mcplock, mcp-warden, mcpward, mcp-hangar `pin --check`); AgentGate was taken because it is the deferred candidate under evaluation, Node-native, and bundles the `deps` check.

**Note 2026-10-30:** **mcp-digest-vectors** (02) publishes 45 before/after `tools/list` vectors with known-answer digests (RFC 8785 + SHA-256, full tool object). If agentgate is trialled, run `agentgate.lock` generation and `ci` against them: duplicate JSON keys must be rejected (a last-wins parser pins the safe text), and the lock must cover the whole tool object, not just the description. No change to agentgate itself.

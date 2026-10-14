# notary-mcp

```json
{
  "id": "notary-mcp",
  "name": "notary-mcp",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/salmanneedsajob/notary-mcp"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "MCP propose → RFC 8785 canonicalize → domain-separated revision hash → human approves exact bytes → fail-closed execute; borrow the content-addressed consent pattern for deliver:* side effects. Watching — demo/hackathon extract, overlaps Spec Guard's hash binding.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-14"
}
```

**notary-mcp** -- MCP approval gate where the human approves a **hash**, not a promise (MIT). Agent proposes an action; server normalizes to canonical bytes (RFC 8785 JSON canonicalization, NFC, surrogate rejection, whitespace collapse), hashes a domain-separated *reviewed revision*; human reviews a field-by-field manifest and approves that revision; `execute_*` takes the revision and refuses wrong hash, drifted draft, superseded/consumed approval. Idempotent via client `operation_id` + server input fingerprint. Ships stdio MCP server, human `npm run review` CLI, and `npm run prove` (56 adversarial checks). Demo action is "publish a post"; pattern claimed for any consequential action. TypeScript, Node ≥20; `package.json` version 1.0.0; **not on npm registry** (local `tsx` run). Repo created/pushed 2026-08-08 04:29 MDT; tip `23fba951676ee7e4538b1131b0f87b0819f08c21`; 0★; extracted from Slopfolio for Push to Prod hackathon.

**Revvel hit:** clearest short README of content-addressed MCP execute consent. Distinct from **agent-approval-check** (merge-side PR humans), **mcp-gate**/**agent-gate** (policy proxy / ship checklist), and closer to **spec-guard**'s hash-bound gates but aimed at *execute exact bytes* rather than Work Packet lifecycle. Borrow the propose→hash→approve→execute contract for deliver:* side effects; do not stand up a second coder pipeline.

**Honesty:** CAN-PARTIAL. Verified 2026-10-14 (America/Denver): GitHub API 200, README + `package.json` read (license MIT declared in `package.json` + README; **no LICENSE file** in repo root, GitHub license field empty), npm `notary-mcp` registry 404. Stale since 2026-08-08 (~2 months), 0★, hackathon extraction — watching only. Prefer **spec-guard** (active) for `spec-approved` and **hashgate** (watching) for Claude Code git/deploy hooks.

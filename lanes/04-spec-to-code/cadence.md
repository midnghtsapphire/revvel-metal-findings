# cadence

```json
{
  "id": "cadence",
  "name": "Cadence",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/thomas-powers-jr/cadence",
    "https://www.npmjs.com/package/@thomas-powers-jr/cadence-core",
    "https://github.com/thomas-powers-jr/cadence/releases/tag/v1.69.1",
    "https://github.com/thomas-powers-jr/cadence/releases/tag/v1.70.0"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "deliver:* — Node/TS settle gate: declared acceptance criteria are re-derived from real evidence (task state, test results, diffs) and `cadence settle run --auto` exits 1 instead of accepting the agent's self-report of done; same engine over CLI, Claude Code/Codex hooks, and `cadence mcp serve`",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-06",
  "updated": "2026-10-12"
}
```

**Cadence** -- verification layer for AI-assisted development. A DRAFT→BUILD→SETTLE loop: work starts with declared acceptance criteria, moves through explicit tasks, and cannot settle until configured quality gates re-check the repo state. The README demo shows an agent gutting a failing assertion to turn CI green; the settle gate still refuses, naming the AC and the dodge, exit 1. One core engine behind three surfaces: the `cadence` CLI, host adapters (Claude Code reference adapter with edit-time boundary gates; Codex), and a stdio MCP server (`cadence mcp serve`, imperative loop only). Gate profiles (`auto` / `standard` / `strict`) control whether `draft approve` needs an interactive human; non-TTY contexts refuse unless explicitly overridden. TypeScript, Node ≥ 22, pnpm/turbo monorepo; MIT; npm **@thomas-powers-jr/cadence-core 1.69.0** (published 2026-10-04); repo tip `0b1c8335a1246ca3cf7614ccd6f0f3615d8db41b` (2026-10-04); ~2★, 19 open issues.

**Revvel hit:** first Node-native entry in this lane, so it sits on the same runtime as the revvel-standards coder path. Use it at the `deliver:*` end: map WR acceptance criteria into Cadence's declared ACs and make `settle run --auto` a required check beside existing CI, so a coder that marks work done without evidence stays red. It is the same existing pipeline with one more check, not a second pipeline. Keep **linebreak-gate** / **spec-guard** as the `spec-approved` human gate; Cadence covers "is done actually done".

**Honesty:** CAN-PARTIAL. Verified 2026-10-06 (America/Denver): GitHub live, MIT LICENSE, npm 1.69.0 live (first publish 2026-08-02). The out-of-box `mock` verifier is deterministic but, per the README, only checks that each AC links to a test, which is not real verification. Real semantic verification goes through an AI verifier (Anthropic, local model, or host CLI), which is non-deterministic, so only the deterministic gates (build/test must pass, task state, diff evidence) should be allowed to block. Very young project with heavy release churn (v1.69 in two months); pin the version.

**Update 2026-10-12:** npm `@thomas-powers-jr/cadence-core` is now **1.70.0** (published 2026-10-10 16:49 MDT). **Pin floor 1.69.1** (release 2026-10-08 18:48 MDT): security patch moving cadence-core's production `@modelcontextprotocol/sdk` dependency from `^1.29.0` to `^1.31.0` for **GHSA-6qxp-vccf-f47h** (high, OAuth client token leak in SDK `>=1.12.0 <1.31.0`; cadence only uses stdio, but the vulnerable client shipped in every install) and pinning the lockfile past `GHSA-jqcg-44mw-7w3h` (critical, `proxy-addr` IP spoofing via the SDK's express). An existing consumer lockfile keeps the old `proxy-addr`, so refresh it, not just the cadence version. 1.70.0 adds read-only `cadence assurance report` (rolls `.cadence/phases/**/*-SUMMARY.json` into ungradable / gradable-ungraded / graded counts, per-gate ran/skipped/not-recorded, bypass counts; `--json` with `schemaVersion`) — usable as a deliver:* evidence artifact. Repo tip `998356d4fff75e4f6ca92d02a8d959c98af63a1c` (2026-10-10); MIT, not archived. Verified 2026-10-12 via npm registry + GitHub releases.

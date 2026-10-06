# cadence

```json
{
  "id": "cadence",
  "name": "Cadence",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/thomas-powers-jr/cadence",
    "https://www.npmjs.com/package/@thomas-powers-jr/cadence-core"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "deliver:* — Node/TS settle gate: declared acceptance criteria are re-derived from real evidence (task state, test results, diffs) and `cadence settle run --auto` exits 1 instead of accepting the agent's self-report of done; same engine over CLI, Claude Code/Codex hooks, and `cadence mcp serve`",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-06"
}
```

**Cadence** -- verification layer for AI-assisted development. A DRAFT→BUILD→SETTLE loop: work starts with declared acceptance criteria, moves through explicit tasks, and cannot settle until configured quality gates re-check the repo state. The README demo shows an agent gutting a failing assertion to turn CI green; the settle gate still refuses, naming the AC and the dodge, exit 1. One core engine behind three surfaces: the `cadence` CLI, host adapters (Claude Code reference adapter with edit-time boundary gates; Codex), and a stdio MCP server (`cadence mcp serve`, imperative loop only). Gate profiles (`auto` / `standard` / `strict`) control whether `draft approve` needs an interactive human; non-TTY contexts refuse unless explicitly overridden. TypeScript, Node ≥ 22, pnpm/turbo monorepo; MIT; npm **@thomas-powers-jr/cadence-core 1.69.0** (published 2026-10-04); repo tip `0b1c8335a1246ca3cf7614ccd6f0f3615d8db41b` (2026-10-04); ~2★, 19 open issues.

**Revvel hit:** first Node-native entry in this lane, so it sits on the same runtime as the revvel-standards coder path. Use it at the `deliver:*` end: map WR acceptance criteria into Cadence's declared ACs and make `settle run --auto` a required check beside existing CI, so a coder that marks work done without evidence stays red. It is the same existing pipeline with one more check, not a second pipeline. Keep **linebreak-gate** / **spec-guard** as the `spec-approved` human gate; Cadence covers "is done actually done".

**Honesty:** CAN-PARTIAL. Verified 2026-10-06 (America/Denver): GitHub live, MIT LICENSE, npm 1.69.0 live (first publish 2026-08-02). The out-of-box `mock` verifier is deterministic but, per the README, only checks that each AC links to a test, which is not real verification. Real semantic verification goes through an AI verifier (Anthropic, local model, or host CLI), which is non-deterministic, so only the deterministic gates (build/test must pass, task state, diff evidence) should be allowed to block. Very young project with heavy release churn (v1.69 in two months); pin the version.

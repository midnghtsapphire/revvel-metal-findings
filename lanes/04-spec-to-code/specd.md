# SpecD

```json
{
  "id": "specd",
  "name": "SpecD (spec-driven development for agents)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/specd-sdd/SpecD",
    "https://getspecd.dev",
    "https://www.npmjs.com/package/@specd/specd"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "research:complete → wr:code / spec-approved: compile relevant specs into coder context; verify plan against requirements before implement — no second spine",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-15"
}
```

Spec-driven development toolkit for AI coding agents. **Context is compiled, not discovered** — at each lifecycle step SpecD assembles the relevant specs + schema instructions into one block. Deterministic where correctness matters (merge, validation, status resolution, delta apply). Plan verification + optional human approval gates before implementation. CLI + core SDK + agent plugins; MCP stub in progress. MIT; npm `@specd/specd` live 2026-09-15.

**Revvel hit:** this is the missing bridge shape after `research:complete` — not another agent runtime. Map SpecD's change lifecycle / schema.yaml onto existing WR labels and `schemas/`. Pair with `issue-15507-closed-as-essay` and Safe Outputs. Do **not** replace `orchestrate.js` or stand up a parallel delivery spine.

**Honesty:** CAN-PARTIAL. GitHub + site + npm verified. Active (updated 2026-09-11). Young; MCP incomplete. Pattern + CLI, not a drop-in for revvel-standards workflows yet.

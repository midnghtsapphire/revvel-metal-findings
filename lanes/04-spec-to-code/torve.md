# Torve

```json
{
  "id": "torve",
  "name": "Torve (spec-and-gate engine)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/morzecrew/torve",
    "https://pypi.org/project/torve/0.7.0/",
    "https://github.com/morzecrew/torve/blob/main/CHANGELOG.md",
    "https://morzecrew.github.io/torve/"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Borrow the gate layer only: `torve gates run --base origin/main` (exit code is the outcome) with builtin `scope` (allow/deny globs), `no-test-tampering`, `red-on-base`, `acceptance`, `decisions-reported` gates, and `torve gates check`, a sabotage suite that proves each gate can fail. Graded LOCKED/ASSUMED/OPEN decisions are a useful vocabulary for spec-approved contracts. Its planner/dispatcher/sandbox loop would be a second pipeline: do not adopt it. Pin ==0.7.0 if trialled; no cross-minor promises yet.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-27"
}
```

**Torve** (`morzecrew/torve`, MIT, Morze Technologies; PyPI `torve`, Python 3.13–3.14) is a "specification-and-gate engine for a standing agent team". A reviewed spec document is minted into machine-checkable task contracts; each task inherits the spec's decisions graded **LOCKED** (executor halts on conflict), **ASSUMED** (departs and logs) or **OPEN** (decides and logs), and a gate reads that log, so a silent workaround is a red build. Scope is a contract: allow/deny globs make touching an out-of-scope file a failing gate and make overlapping tasks undispatchable in parallel. Builtin gates: `scope`, `secrets`, `no-test-tampering`, `decisions-reported`, `acceptance`, `red-on-base`, `self-audit`, `source-layout`, `user-facing-text`; anything else is a shell command in `.torve/gates.yaml`. Gates that need a contract report `skipped`, never a silent green. `torve gates check` runs a sabotage suite to prove each gate can fail. Agents run only in Docker sandboxes; a read-only MCP server reports attempts, costs and escalations back to planning. **0.7.0** (PyPI 2026-10-27 02:59 MDT) adds `torve spec check` warnings when a phase's scope touches a LOCKED row of a `depends_on` document, an `--urgent` halt for a running attempt, and makes the scope gate name whitespace-only out-of-scope edits (still failing).

**Revvel hit:** the smallest useful piece is "gates in CI": a base-relative gate run whose exit code decides, plus a self-test that each gate can actually go red. That maps onto the wr:code → deliver:* check without importing the rest. `red-on-base` (tests must fail on the base before the change) and `no-test-tampering` are cheap, deterministic ideas for revvel's own gate list. Do **not** adopt Torve's planner / night runner / sandboxed seats: that would be a second pipeline. Advisory only.

**Honesty:** CAN-PARTIAL. Verified 2026-10-27 (America/Denver): GitHub repo API (created 2026-08-20, MIT, 0 stars, not archived), raw LICENSE (MIT License, (c) 2026 Morze Technologies), CHANGELOG 0.7.0 entry read, PyPI JSON (13 releases; 0.1.0 2026-10-04; 0.7.0 2026-10-27), PyPI/docs/repo pages 200. Not run. The README itself calls it an alpha with one operator and one adopter, run on Linux + Docker with Claude Code; nothing is promised across minor releases; each upgrade needs image rebuilds and sometimes migrations.

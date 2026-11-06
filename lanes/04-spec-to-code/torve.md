# Torve

```json
{
  "id": "torve",
  "name": "Torve (spec-and-gate engine)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/morzecrew/torve/releases/tag/v0.9.1",
    "https://github.com/morzecrew/torve/releases/tag/v0.9.0",
    "https://github.com/morzecrew/torve/releases/tag/v0.8.0",
    "https://github.com/morzecrew/torve",
    "https://pypi.org/project/torve/0.7.0/",
    "https://github.com/morzecrew/torve/blob/main/CHANGELOG.md",
    "https://morzecrew.github.io/torve/"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Borrow the gate layer only: `torve gates run --base origin/main` (exit code is the outcome) with builtin `scope`, `no-test-tampering`, `red-on-base`, `acceptance`, `decisions-reported` gates, and `torve gates check` (sabotage suite proving each gate can fail). New in 0.8.0: `@suite` gate rule, a failing test convicts only if red at head and not red on the merge base (inherited reds recorded, never convict), and an `evidence` shadow gate naming each decision row no changed test proves. Its planner/night runner/sandbox loop would be a second pipeline: do not adopt it. Pin ==0.8.0 if trialled; 0.9.0/0.9.1 stay on contract v3 (critic review, $3/90min critic defaults in 0.9.1) — wait.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-27"
}
```

**Torve** (`morzecrew/torve`, MIT, Morze Technologies; PyPI `torve`, Python 3.13–3.14) is a "specification-and-gate engine for a standing agent team". A reviewed spec document is minted into machine-checkable task contracts; each task inherits the spec's decisions graded **LOCKED** (executor halts on conflict), **ASSUMED** (departs and logs) or **OPEN** (decides and logs), and a gate reads that log, so a silent workaround is a red build. Scope is a contract: allow/deny globs make touching an out-of-scope file a failing gate and make overlapping tasks undispatchable in parallel. Builtin gates: `scope`, `secrets`, `no-test-tampering`, `decisions-reported`, `acceptance`, `red-on-base`, `self-audit`, `source-layout`, `user-facing-text`; anything else is a shell command in `.torve/gates.yaml`. Gates that need a contract report `skipped`, never a silent green. `torve gates check` runs a sabotage suite to prove each gate can fail. Agents run only in Docker sandboxes; a read-only MCP server reports attempts, costs and escalations back to planning. **0.7.0** (PyPI 2026-10-27 02:59 MDT) adds `torve spec check` warnings when a phase's scope touches a LOCKED row of a `depends_on` document, an `--urgent` halt for a running attempt, and makes the scope gate name whitespace-only out-of-scope edits (still failing).

**Revvel hit:** the smallest useful piece is "gates in CI": a base-relative gate run whose exit code decides, plus a self-test that each gate can actually go red. That maps onto the wr:code → deliver:* check without importing the rest. `red-on-base` (tests must fail on the base before the change) and `no-test-tampering` are cheap, deterministic ideas for revvel's own gate list. Do **not** adopt Torve's planner / night runner / sandboxed seats: that would be a second pipeline. Advisory only.

**Honesty:** CAN-PARTIAL. Verified 2026-10-27 (America/Denver): GitHub repo API (created 2026-08-20, MIT, 0 stars, not archived), raw LICENSE (MIT License, (c) 2026 Morze Technologies), CHANGELOG 0.7.0 entry read, PyPI JSON (13 releases; 0.1.0 2026-10-04; 0.7.0 2026-10-27), PyPI/docs/repo pages 200. Not run. The README itself calls it an alpha with one operator and one adopter, run on Linux + Docker with Claude Code; nothing is promised across minor releases; each upgrade needs image rebuilds and sometimes migrations.

**Update 2026-11-05 -- 0.8.0 and 0.9.0 (MIT):** GitHub releases **v0.8.0** (2026-11-04 08:15 MST) and **v0.9.0** (2026-11-05 07:04 MST). 0.8.0 adds the `@suite` gate (whole suite once; a failing test convicts only when it is red at the head and not red on the merge base, a red the base also carries is recorded as inherited), the `evidence` shadow gate (names each decision row that no changed test proves by failing on base and passing on the candidate), a `lane.judged` record per battery, `fixes` headers that become `Closes` lines, and label-gated issue intake (only if the labeller holds triage+ and the issue was not edited after labelling). 0.9.0 adds an optional `review.mode: critic` (frozen prompt; the engine blocks on located findings, never the stated verdict), `.torve/review/evidence.yaml`, a review corpus with gaming cases (weak test, test edited to pass, code special-casing `PYTEST_CURRENT_TEST`), and `torve abort --claim --evidence`; it changes contracts to version 3 and runs row checks only when a document completes. Both need every host sharing a store upgraded together.

**Revvel hit (2026-11-05):** the inherited-red rule is the cheapest borrow yet: revvel's deliver:* gate should convict a PR only for tests that are red at the head **and** green on the merge base, so a flaky or pre-broken main does not block a clean WR. The three gaming cases are good fixtures for revvel's own `no-test-tampering` check. Pin ==0.8.0 for any gate trial; skip 0.9.0 until contract v3 settles.

**Honesty (2026-11-05):** CAN-PARTIAL. Verified 2026-11-05 (America/Denver): GitHub releases API bodies and publish times for v0.8.0 and v0.9.0; repo API (MIT, pushed 2026-11-05). Not run.

**Update 2026-11-06 -- 0.9.1 (still skip):** GitHub / PyPI **v0.9.1** (2026-11-06 01:20 MST / 08:20 UTC). Critic-mode defaults: stop a unit at **$3** notional spend across attempts (`budget_exhausted`); default **90 minutes** wallclock when the contract omits `budget.wallclock_minutes`. Review-finding fixes (last-review-only rounds, findings without cited lines anchor to phased landed files, empty worktrees judged at HEAD, timeout kills child processes, `spec archive` keeps `execution/` landings). Still the contract-v3 / critic family from 0.9.0.

**Revvel hit (2026-11-06):** pin stays **==0.8.0** for any gate trial; skip 0.9.1 with 0.9.0 until contract v3 settles. The $3 / 90min critic budgets are irrelevant while the planner/critic loop is out of scope.

**Honesty (2026-11-06):** CAN-PARTIAL. Verified 2026-11-06 (America/Denver): GitHub releases API body v0.9.1 publish 2026-11-06T08:20:18Z; raw CHANGELOG 0.9.1; PyPI torve 0.9.1 upload 2026-11-06T08:19:49Z; release page 200. Not run.


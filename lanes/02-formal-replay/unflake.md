# unflake

```json
{
  "id": "unflake",
  "name": "unflake — Deterministic Simulation Testing for TypeScript",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/BOTIROFF-D/unflake",
    "https://www.npmjs.com/package/unflake"
  ],
  "license": "MIT",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "scripts/ + TESTING_STANDARD.md — shrinkable seed/plan replay for orchestrate.js / label-graph async races (Node), peer to chronos-dst",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-17"
}
```

Zero-dependency TypeScript DST. Patches timers / `Date` / `Math.random`, explores macrotask interleavings from a seed, **shrinks** failures to a minimal plan, and can **`explore` exhaustively** on small spaces (`exhaustive: true` = no failure in the model). Same seed ⇒ byte-identical run; `plan` / `planStrict` replays without the seed. npm `unflake` 0.3.0 + GitHub verified live this scrape.

Unlike Chronos, unflake does **not** simulate networks/partitions/crashes — it owns schedule + virtual time + shrink/exhaust. That is the right shape for label-graph races (double-lease, stale write, lock-order, retry-double-charge) without pulling a full chaos stack.

**Revvel hit:** pair with `chronos-dst` / `tigerbeetle-dst` method — Chronos when you need network/entropy capsules; unflake when you need shrinkable plans and exhaustive small proofs on the Node orchestrator. Same seed, same miss. Not a second pipeline — a language-matched harness for `wr:code` / `spec-approved` / `deliver:*` transitions.

**Honesty:** CAN-PARTIAL. GitHub + npm verified. Young (0★; ~8 weekly downloads). No network DST. Treat as method transfer for async races, not a vendor lock-in.

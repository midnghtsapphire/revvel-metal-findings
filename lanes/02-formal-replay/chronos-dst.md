# Chronos (Node/TS DST)

```json
{
  "id": "chronos-dst",
  "name": "Chronos — Deterministic Simulation Testing for Node.js / TypeScript",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/sx4im/chronos",
    "https://www.npmjs.com/package/@sx4im/chronos-core"
  ],
  "license": "MIT",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "scripts/ + TESTING_STANDARD.md — seed-replay harness for orchestrate.js / label graph in the stack language (Node), not Zig",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-15"
}
```

TigerBeetle / FoundationDB-style DST, built natively for **Node.js & TypeScript**. Virtual clock, seeded PRNG (`xoshiro256**`), simulated network (latency, loss, partitions, crash/restart), entropy guards that fail if `Date.now()` / `Math.random()` / real `setTimeout` escape. Same seed ⇒ bit-for-bit replay. Vitest-native packages (`@sx4im/chronos-core`, `@sx4im/chronos-vitest`). Repo + npm live 2026-09-15; README claims MIT.

**Revvel hit:** steal TigerBeetle's *method* (already in `tigerbeetle-dst`) but run it where the orchestrator actually lives. Stub GitHub events, time, OpenRouter; assert the label graph (`research:complete` → `wr:code` / `spec-approved` → `deliver:*`). Same seed, same miss. Chronos is the JS twin — not a second pipeline, a language-matched harness.

**Honesty:** CAN-PARTIAL. GitHub + npm verified. Young project (~19★); treat as method transfer, not a vendor lock-in.

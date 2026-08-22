# TigerBeetle Deterministic Simulation Testing (VOPR)

```json
{
  "id": "tigerbeetle-dst",
  "name": "TigerBeetle VOPR / protocol-aware DST",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://tigerbeetle.com/blog/2026-08-20-protocol-aware-dst/",
    "https://github.com/tigerbeetle/tigerbeetle/blob/main/docs/internals/vopr.md"
  ],
  "license": "Apache-2.0 (TigerBeetle)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "scripts/ + TESTING_STANDARD.md — seed-replay harness for orchestrate.js",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Production consensus/storage code runs in a single process. Clock, disk, network are models. Seed + git commit replay the exact failure. Protocol-aware DST (posted 2026-08-20) inspects per-replica consensus state, not just black-box linearizability. Companion Vortex is the *non*-deterministic outside-in harness.

**Revvel hit:** the orchestrator and research-engine are already "who goes next" machines. They fail silently (missing `wr:code`). A tiny DST: stub GitHub events, time, OpenRouter, assert the label graph. Same seed, same miss. That is how you make the healers honest.

**Do not** import TigerBeetle itself. Steal the *method*: seed, virtual time, injectable I/O, state checker.

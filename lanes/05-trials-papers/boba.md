# boba

```json
{
  "id": "boba",
  "name": "BOBA-Bench: chained coding requests collapse without external verification",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.02207",
    "https://github.com/amazon-agi/BOBA-bench",
    "https://amazon-agi.github.io/BOBA-bench/"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Evidence for keeping an external, deterministic check between every wr:code -> deliver:* step and never letting the coder's own tests or self-review close a WR: on chains of 20 dependent requests, ten agents finished 95% of requests alone but 51% of chains; one external 'verification failed' plus one repair round raised it to 59%. Supports attested / cadence / agent-approval-check as required checks per WR, not per batch. Benchmark only; no adoption.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-03"
}
```

**Built on Broken Assumptions (BOBA): Why Coding Agents Cannot Be Left Alone** (Alejandro Cuadron, Arpit Gupta; Amazon). arXiv **2611.02207** v1, submitted 2026-11-01 14:06 MST. Code + data: `amazon-agi/BOBA-bench` (Apache-2.0 per repo API; created 2026-11-03 02:17 MST, 0 stars, no release); site `amazon-agi.github.io/BOBA-bench`.

Benchmark: 280 chains x 20 consecutive requests from 140 real repositories (contiguous commit history); each request in a fresh conversation on the code the earlier requests left; hidden tests grade every request; the agent is never told a verdict.

Authors' numbers: ten agents complete 95% of requests one at a time but 51% when chained; checked agent code is nearly as good a base as human code, so the cause is missed mistakes: agents declare done once their own tests pass, the next request then fails about twice as often, and agents asked to review an implementation are right 53% of the time. One external "that's wrong" after a failed request plus one repair round lifts chain completion 51% -> 59%.

**Revvel hit:** revvel-standards runs WRs as a chain on one repo. This is direct evidence that the coder's self-report and self-review must not close a WR; an external check (repo's own tests via attested, cadence's evidence gate, a fresh-context verifier per who-verifies-builder) must sit on every wr:code -> deliver:* step, with its failure fed back once. Fits the existing required-checks list; no new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-03 (America/Denver): arXiv export API metadata + abstract (code link in comment), abs page 200; repo API (Apache-2.0, created date), README read via API, site 200. Not run. Results are the authors'.

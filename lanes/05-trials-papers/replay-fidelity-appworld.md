# replay-fidelity-appworld

```json
{
  "id": "replay-fidelity-appworld",
  "name": "Replay Fidelity in LLM Agent Evaluation: Randomness, Hidden State, and Test Oracles in AppWorld",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.11216"
  ],
  "license": "n/a (paper; no code URL found)",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Replay-lane rule for wr:code fixtures: reset the RNG before every interaction (fixed-code replay admission went 42 -> 68 of 71 runs) and compare state deltas / oracle verdicts, not printed output — four materialized-state discrepancies hid behind matching outputs and verdicts. Applies to the committed-fixture replay (chronicle / agentverify cassettes); no new pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-10"
}
```

**Replay Fidelity in LLM Agent Evaluation** (You Liu, Quanchao Lu). arXiv **2611.11216** v1, submitted 2026-11-08. Audits all 71 unsuccessful executions in a fixed historical AppWorld corpus with 284 isolated fixed-code replay attempts. Reconstructed declared settings admit 42 cases under printed-output, pre-oracle DB-delta and native-verdict checks; resetting the RNG before each interaction admits 68. Under DB/oracle checks the 26-case gap shrinks to four. Found materialized-state differences despite matching outputs and verdicts (same API call, same response, different row effects), plus JWT credential-equality and auth/write differences. A 12-case BFCL pilot showed no discrepancy. Bounded empirical study; no claims about debugger accuracy or repair gains.

**Revvel hit:** when wr:code runs are replayed from fixtures, the comparison has to include side-effect state (files/DB/labels touched), and nondeterminism sources (RNG, time, tokens) must be pinned per interaction, not per run.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-10 (America/Denver): arXiv export API abstract + comment; abs page HTTP 200; HTML v1 returned 404 (not yet rendered), so no code URL could be checked. Not run.

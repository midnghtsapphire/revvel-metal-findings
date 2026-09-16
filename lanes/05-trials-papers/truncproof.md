# TruncProof — JSON + Token-Budget Guardrail

```json
{
  "id": "truncproof",
  "name": "TruncProof",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2605.13076",
    "https://github.com/Yosshi999/TruncProof"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "deliver:* JSON WR dumps under hard max_tokens — stop truncated invalid JSON",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-16"
}
```

IJCNN 2026. LL(1) JSON grammar-constrained decoding that also tracks **minimum tokens-to-accept**, so the mask blocks tokens that would make a valid completion impossible inside `N_max`. Fixes the silent failure mode where ordinary GCD stays prefix-feasible until the budget cuts mid-object.

Public MIT repo (`Yosshi999/TruncProof`) with sample script, Docker repro, and MCTS/beam variants.

**Revvel hit:** when `deliver:*` / Project v2 JSON must finish inside a hard token ceiling, TruncProof-style remaining-cost masks sit in front of the existing structured-output path — not a second coder pipeline.

**Honesty:** paper + GitHub verified live; research-grade, not a vLLM/XGrammar production backend.

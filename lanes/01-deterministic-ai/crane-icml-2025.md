# CRANE — Constrained Reasoning Augmented Generation

```json
{
  "id": "crane-icml-2025",
  "name": "CRANE (ICML 2025)",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2502.09061",
    "https://proceedings.mlr.press/v267/banerjee25a.html"
  ],
  "license": "UNKNOWN (paper; code link from abs page)",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "research-engine + openrouter-coder: CoT unconstrained, final label/JSON constrained",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-27"
}
```

ICML 2025. Strict grammar masks can kill reasoning. CRANE alternates: unconstrained windows for CoT, constrained windows for structural answers, toggled by delimiter symbols (`<<` / `>>` in their evals).

Up to ~10pp accuracy over pure constrained or unconstrained on GSM-Symbolic / FOLIO while keeping parse rates high.

**Not** the 2026 NeurIPS “nullspace editing” CRANE (different paper, same acronym).

**Revvel hit:** research dumps and viability gates need free reasoning *and* schema-valid finals. Pattern for `OUTPUT_TYPE` / label JSON: reason free, emit the enum/object under mask. Pair with LLGuidance or XGrammar as the CSD backend — CRANE is the switch policy, not a new mask engine.

**Honesty:** theory + evals verified on arXiv/PMLR. No claim that OpenRouter exposes logit masks for this switch today.

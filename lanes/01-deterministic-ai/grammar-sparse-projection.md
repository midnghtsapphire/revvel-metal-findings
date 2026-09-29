# grammar-sparse-projection (GSP)

```json
{
  "id": "grammar-sparse-projection",
  "name": "GSP (Grammar-Conditioned Sparse Projection)",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/StealthEyeLLC/grammar-sparse-projection",
    "https://github.com/StealthEyeLLC/grammar-sparse-projection/releases/tag/v0.1.1",
    "https://github.com/sgl-project/sglang/discussions/41638"
  ],
  "license": "Apache-2.0",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Cage / openrouter-coder structured JSON — Triton sparse LM-head behind xgrammar-2 masks when self-hosting; pairs with cfgzip; not a second spine",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-29"
}
```

**GSP** -- Grammar-Conditioned Sparse Projection. Research prototype (MLSys 2027 target) that uses a grammar's packed legal-token mask to **skip LM-head work** for illegal vocabulary regions instead of computing full logits then masking. Exact in constrained support: `softmax(W_A h)` vs dense `softmax(mask(W h))`. Live modules `gsp/runtime.py` + `gsp/triton_runtime.py`: packed-bitmask row-sparse (batch-1) + grammar-aware block GEMM (batched) + density dispatcher that falls back to dense LM head + stock XGrammar when sparsity is unprofitable. Apache-2.0 software; CC BY 4.0 paper; **v0.1.1** released 2026-09-29; 0★ at acquire; deps `transformers==5.17.0`, `xgrammar==0.2.8`, `triton==3.7.1`. Qwen3.5-2B (248k vocab) paired AB/BA: ~1.06–1.08× end-to-end on enum/tool/nested JSON vs dense+XGrammar; batched LM-head ~2.5–4.6× on highly constrained requests. Free-string control not a reliable win. Asks for vLLM/SGLang integration replications (SGLang discussion #41638 live).

**Revvel hit:** when self-hosting the schema cage for `wr:code` / `deliver:*` dumps under **xgrammar-2**, GSP is the near-metal path that makes grammar masks cheap at the **head**, complementary to **cfgzip** (vocab equivalence compression before the engine). Keep **llguidance** on the paid OpenRouter path. Do not invent a second serving pipeline — swap the projection behind the existing mask contract. Pair honesty with **cd-scale-semantic-gap**: faster schema ≠ semantics.

**Honesty:** CAN-PARTIAL. Verified 2026-09-29 (America/Denver): GitHub live (Apache-2.0 LICENSE, CITATION.cff 0.1.1, `gsp/` + `tests/` + `benchmarks/` + `results/`); release tag `v0.1.1` 200; SGLang discussion 200. Transformers+XGrammar research path today — **no** production vLLM/SGLang plugin yet (explicitly solicited). Modest e2e gains on laptop RTX; datacenter replication pending. Not a pip package (requirements.txt + local `gsp/`).

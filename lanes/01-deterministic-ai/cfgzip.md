# CFGzip

```json
{
  "id": "cfgzip",
  "name": "CFGzip",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/mjs227/cfgzip",
    "https://github.com/coli-saar/cfgzip-rust",
    "https://pypi.org/project/cfgzip/",
    "https://arxiv.org/abs/2605.29986",
    "https://github.com/coli-saar/cfgzip-experiments"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Accelerate self-hosted XGrammar-2 masks on static complex WR/code grammars — lossless class vocab so mask tax drops without a second decoder pipeline",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-21"
}
```

Offline **token-vocabulary compression** layer for CFG-constrained decoding. Precomputes equivalence classes for a fixed `(grammar, tokenizer)` pair so the grammar engine (today: **XGrammar2**) masks over ~1–3k class representatives instead of 100–200k tokens; `MaskTranslator` expands the class mask back to the full vocab. Claims **lossless** (byte-identical to unmodified engine) and up to **~7.5×** end-to-end speedup on complex CFGs (C++/Bython-class) vs XGrammar2 alone; JSON schemas already cheap so payoff is smaller there. Pip `cfgzip==0.1.1` (`pip install "cfgzip[xgrammar]"`); GBNF grammars; `XgrammarProcessor` is a transformers `LogitsProcessor`. README: intended for **static, reused** large grammars — not per-request dynamic schemas.

**Revvel hit:** when a self-hosted coder already pins XGrammar (see **xgrammar-2**) on a stable WR/code GBNF, CFGzip is the drop-in accelerator — preprocess once, cache `EquivalenceClassData`, keep the same schema contract. Do **not** open a second structured-output path; wrap the existing mask engine. Vendor/OpenRouter paths stay on **llguidance**.

**Honesty:** CAN-PARTIAL. Verified 2026-09-21: GitHub `mjs227/cfgzip` live (4★, Apache-2.0 LICENSE + pyproject), PyPI `cfgzip` 0.1.1 live, arXiv 2605.29986 live, experiments mirror `coli-saar/cfgzip-experiments` live. Re-verified 2026-09-22: companion **`coli-saar/cfgzip-rust`** live (Apache-2.0) — Rust CLI `cfgzip-preprocess` is now the recommended offline preprocessor; Python preprocess deprecated. Backend today is still **XGrammar2 only** (`BaseProcessor` extension point; llguidance planned). **Still not** a native vLLM/SGLang plugin — transformers generate path only. Not a PSC successor. Offline precompute can take minutes; wrong tool for one-shot dynamic JSON schemas.

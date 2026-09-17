# GLRMask

```json
{
  "id": "glrmask",
  "name": "GLRMask",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/IsaacBreen/glrmask",
    "https://pypi.org/project/glrmask/",
    "https://crates.io/crates/glrmask",
    "https://docs.rs/glrmask"
  ],
  "license": "MIT OR Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Local / research-engine mask cage for schema-valid wr:code JSON — MaskBench TBM tails beat LLGuidance claims; not a vLLM drop-in",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-17"
}
```

Rust + Python grammar-constrained decoding library. Compiles JSON Schema / GLRM / Lark / EBNF against a model vocabulary into a reusable `Constraint`; runtime is `mask()` + `commit_token()`. Supports `DynamicConstraint` for cold-start, `save()`/`load()` of compiled artifacts, and composable `extern grammar` / special-token binds. Live on GitHub, PyPI (`glrmask` 0.1.1), and crates.io this scrape.

Author engineering run (JSONSchemaBench / MaskBench, Aug 2026) claims **TBM p50 3 µs / p99 10 µs / max 70 µs** vs LLGuidance **10 / 223 / 14,426 µs** on the same corpus — at the cost of **much higher TTFM** (compile) than LLGuidance. Interim numbers; README says not the final publication benchmark.

**Revvel hit:** when you self-host a research or llama.cpp coder and need hard schema masks for WR / `wr:code` dumps, GLRMask is the strongest *library* peer to Outlines with better claimed mask tails. Keep LLGuidance / XGrammar on the vendor and vLLM paths you already pay for — do not invent a second pipeline; swap the mask engine behind the existing coder contract.

**Honesty:** CAN-PARTIAL. Repo + PyPI + crates.io + docs.rs verified live 2026-09-17. No vLLM / SGLang / OpenRouter backend found. Young (0★ GitHub; PyPI ~277 downloads/mo). Treat as local twin / MaskBench contender, not production serving.

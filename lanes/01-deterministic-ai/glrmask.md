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
    "https://docs.rs/glrmask",
    "https://github.com/IsaacBreen/glrmask/releases/tag/v0.2.0"
  ],
  "license": "MIT OR Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Local / research-engine mask cage for schema-valid wr:code JSON — MaskBench TBM tails beat LLGuidance claims; not a vLLM drop-in; pin glrmask ==0.2.0 (breaking API vs 0.1.1; rebuild cached artifacts)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-17"
}
```

Rust + Python grammar-constrained decoding library. Compiles JSON Schema / GLRM / Lark / EBNF against a model vocabulary into a reusable `Constraint`; runtime is `mask()` + `commit_token()`. Supports `DynamicConstraint` for cold-start, `save()`/`load()` of compiled artifacts, and composable `extern grammar` / special-token binds. Live on GitHub, PyPI (`glrmask` 0.1.1), and crates.io this scrape.

Author engineering run (JSONSchemaBench / MaskBench, Aug 2026) claims **TBM p50 3 µs / p99 10 µs / max 70 µs** vs LLGuidance **10 / 223 / 14,426 µs** on the same corpus — at the cost of **much higher TTFM** (compile) than LLGuidance. Interim numbers; README says not the final publication benchmark.

**Revvel hit:** when you self-host a research or llama.cpp coder and need hard schema masks for WR / `wr:code` dumps, GLRMask is the strongest *library* peer to Outlines with better claimed mask tails. Keep LLGuidance / XGrammar on the vendor and vLLM paths you already pay for — do not invent a second pipeline; swap the mask engine behind the existing coder contract.

**Honesty:** CAN-PARTIAL. Repo + PyPI + crates.io + docs.rs verified live 2026-09-17. No vLLM / SGLang / OpenRouter backend found. Young (0★ GitHub; PyPI ~277 downloads/mo). Treat as local twin / MaskBench contender, not production serving.

**Update 2026-10-13:** **GLRMask 0.2.0** released (GitHub release 2026-10-10 08:04 MDT; PyPI `glrmask` 0.2.0 uploaded 2026-10-10 03:33 MDT; crates.io `glrmask` max version 0.2.0). Built from commit `9ef50c988199e2c7bcba6c29d44e5ecae5ceb2f3`. **Breaking API change from 0.1.1**: immutable grammar descriptions, reusable `UnlinkedConstraint` components, runnable `Constraint`, per-sequence `ConstraintState`. Build presets are `FastBuild` (Dynamic/O1), `Balanced` (native O2), `FastRuntime` (Static), and `Auto` (default). `is_terminated()` is **removed**: generation stops at the first accepting match or at a configured end token, and an allowed end-token commit empties the next mask while preserving acceptance. The release fixes exact Lark whole-word masks for compressed direct-regular languages. Serialized artifacts are still pre-release formats and **may need rebuilding**. Wheels cover CPython 3.9–3.13 (manylinux x86_64/aarch64, macOS, Windows x86_64); Python 3.14 is outside the tested matrix. The release states the August MaskBench numbers above are a historical interim run, **not** a measurement of 0.2.0, and makes no new performance claim. A verification manifest + `SHA256SUMS` are attached. For revvel: if a local twin uses GLRMask, pin `==0.2.0`, port any `is_terminated()` loop to end-token handling, and rebuild cached constraints. Still no vLLM/SGLang backend. Repo pushed 2026-10-12 23:03 MDT. Verified 2026-10-13 (America/Denver) via the GitHub releases API, PyPI JSON, and the crates.io API (crates.io web page 404s the fetcher; API is the receipt).

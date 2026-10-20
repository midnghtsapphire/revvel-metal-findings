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
    "https://github.com/IsaacBreen/glrmask/releases/tag/v0.3.1",
    "https://www.npmjs.com/package/@glrmask/node",
    "https://glrmask.com/api/javascript/"
  ],
  "license": "MIT OR Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Local / research-engine mask cage for schema-valid wr:code JSON; not a vLLM drop-in. Since 0.3.1 also a Node-API package (`@glrmask/node`) and a C/C++ ABI, so a local Node coder next to orchestrate.js can mask in-process instead of via Python. Pin glrmask ==0.3.1 (0.3.0 breaks the 0.2.0 API again; older private artifacts are rejected, rebuild them)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-17",
  "updated": "2026-10-20"
}
```

Rust + Python grammar-constrained decoding library. Compiles JSON Schema / GLRM / Lark / EBNF against a model vocabulary into a reusable `Constraint`; runtime is `mask()` + `commit_token()`. Supports `DynamicConstraint` for cold-start, `save()`/`load()` of compiled artifacts, and composable `extern grammar` / special-token binds. Live on GitHub, PyPI (`glrmask` 0.1.1), and crates.io this scrape.

Author engineering run (JSONSchemaBench / MaskBench, Aug 2026) claims **TBM p50 3 µs / p99 10 µs / max 70 µs** vs LLGuidance **10 / 223 / 14,426 µs** on the same corpus — at the cost of **much higher TTFM** (compile) than LLGuidance. Interim numbers; README says not the final publication benchmark.

**Revvel hit:** when you self-host a research or llama.cpp coder and need hard schema masks for WR / `wr:code` dumps, GLRMask is the strongest *library* peer to Outlines with better claimed mask tails. Keep LLGuidance / XGrammar on the vendor and vLLM paths you already pay for — do not invent a second pipeline; swap the mask engine behind the existing coder contract.

**Honesty:** CAN-PARTIAL. Repo + PyPI + crates.io + docs.rs verified live 2026-09-17. No vLLM / SGLang / OpenRouter backend found. Young (0★ GitHub; PyPI ~277 downloads/mo). Treat as local twin / MaskBench contender, not production serving.

**Update 2026-10-13:** **GLRMask 0.2.0** released (GitHub release 2026-10-10 08:04 MDT; PyPI `glrmask` 0.2.0 uploaded 2026-10-10 03:33 MDT; crates.io `glrmask` max version 0.2.0). Built from commit `9ef50c988199e2c7bcba6c29d44e5ecae5ceb2f3`. **Breaking API change from 0.1.1**: immutable grammar descriptions, reusable `UnlinkedConstraint` components, runnable `Constraint`, per-sequence `ConstraintState`. Build presets are `FastBuild` (Dynamic/O1), `Balanced` (native O2), `FastRuntime` (Static), and `Auto` (default). `is_terminated()` is **removed**: generation stops at the first accepting match or at a configured end token, and an allowed end-token commit empties the next mask while preserving acceptance. The release fixes exact Lark whole-word masks for compressed direct-regular languages. Serialized artifacts are still pre-release formats and **may need rebuilding**. Wheels cover CPython 3.9–3.13 (manylinux x86_64/aarch64, macOS, Windows x86_64); Python 3.14 is outside the tested matrix. The release states the August MaskBench numbers above are a historical interim run, **not** a measurement of 0.2.0, and makes no new performance claim. A verification manifest + `SHA256SUMS` are attached. For revvel: if a local twin uses GLRMask, pin `==0.2.0`, port any `is_terminated()` loop to end-token handling, and rebuild cached constraints. Still no vLLM/SGLang backend. Repo pushed 2026-10-12 23:03 MDT. Verified 2026-10-13 (America/Denver) via the GitHub releases API, PyPI JSON, and the crates.io API (crates.io web page 404s the fetcher; API is the receipt).

**Update 2026-10-19:** **GLRMask 0.3.0** (PyPI 2026-10-16 22:01 MDT; tag `v0.3.0`, no GitHub release object) and **0.3.1** (GitHub release "C++ and JavaScript bindings" 2026-10-17 23:37 MDT, commit `e8b5e6a59ca7aec336c929b7d27d5fcfcf5a1363`; PyPI 2026-10-18 00:55 MDT; crates.io max 0.3.1; npm `@glrmask/node` 0.3.1 2026-10-18 00:08 MDT, `MIT OR Apache-2.0`).

- **0.3.0 is another breaking API change** (`CHANGELOG.md` at `v0.3.1`): lifecycle is now `Grammar` → `PreparedGrammar` → `Constraint` → `ConstraintState`; the public `UnlinkedConstraint` / `compile_unlinked` spellings from 0.2.0 are gone; `bind()` is a single-item mutation; `forced()` / `forced_token_ids()` removed in favour of `forced_tokens()`; prepared assemblies stored as a bounded DAG and **older private artifact versions are rejected** rather than upgraded. Grammar frontends: layout-independent native GLRM, documented Lark recognition profile and an explicit LLM compatibility profile. Python type stubs + `py.typed`. Adds `docs/validation/core-batch-2026-10-15.md` (matched core-batch qualification results with stated performance/scaling limits; not read in full this run).
- **0.3.1 adds native bindings:** C ABI + C++17 RAII (CMake, static/shared libs, release tarballs for Linux x64/arm64, macOS x64/arm64, Windows x64) and a **Node-API package `@glrmask/node`** (CJS + ESM, TypeScript declarations, async compilation, packed token masks). Trusted publishing to npm, PyPI, crates.io. Browser Wasm is a separate future target.
- Paper: "GLRMask: Constrained Decoding with Boolean Array Weighted Automata" (Zenodo preprint, 2026-10-09, DOI 10.5281/zenodo.23273555; Zenodo/DOI pages 403 the fetcher, so the numbers below are from the search-index abstract only): Static GLRMask TBM p50 2.54 µs / p99 9.54 µs / max 59.3 µs vs llguidance 8.71 µs / 379.6 µs / 7.84 ms on 2,925,983 JSONSchemaBench positions. Single author; not peer-reviewed.

**Revvel hit (2026-10-19):** the Node binding matters because the repo's host is Node (`orchestrate.js`, `scripts/local_llm.js`): a local twin could mask in-process like **vocab-mask-trie** but with full CFG/JSON-Schema support. Still no vLLM/SGLang backend. Pin `==0.3.1`, port 0.2.0 code to the `PreparedGrammar` lifecycle, rebuild cached artifacts.

**Honesty (2026-10-19):** CAN-PARTIAL. Verified 2026-10-19 (America/Denver): GitHub releases + tags API, raw `CHANGELOG.md` at `v0.3.1`, PyPI JSON (0.3.0, 0.3.1), crates.io API (0.3.1), npm registry JSON for `@glrmask/node`, release page and `glrmask.com/api/javascript/` 200 (npmjs.com web 403s the fetcher, as elsewhere). GitHub's license detector shows Apache-2.0; package metadata says `MIT OR Apache-2.0`. Very young (1★). Fast-moving API: two breaking minors in nine days.

**Update 2026-10-20:** no new published release (PyPI, crates.io, npm `@glrmask/node` all still **0.3.1**). `main` moved fast overnight: a **GLRMask 0.4.0 release candidate** is merged as "unpublished" metadata (2026-10-19 22:14 MDT) with a new configured `Module` graph + scope-preserving `Expr` API across bindings, "native shortest syntax" removed, the relocated CMake consumer requirement bumped to 0.4, and a `rand` 0.8.6 soundness advisory patched in the RC; latest commit 2026-10-20 04:55 MDT merges an opt-in full-JSON fix accepting member permutations of small (2–3 key) closed objects while keeping llguidance canonical ordering as the default. Expect a third breaking minor; keep `==0.3.1` until 0.4.0 publishes and re-read its CHANGELOG then. Verified via registry JSON and the GitHub commits API, 2026-10-20 (America/Denver).

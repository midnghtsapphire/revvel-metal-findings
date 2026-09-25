# Trie Automata (finite-set constrained decoding)

```json
{
  "id": "trie-automata",
  "name": "Trie Automata",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2608.12574",
    "https://arxiv.org/pdf/2608.12574"
  ],
  "license": "unknown",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Large-K deliver:* / tool-enum allowlists -- claimed vLLM LogitsProcessor path (29x batch vs XGrammar); watch for code drop vs STATIC",
  "honesty": "WATCH",
  "acquired": "2026-09-25"
}
```

**Trie Automata for Constrained Decoding over Large Finite Sets** (Xu & Bouyarmane, Amazon; arXiv 2608.12574, Aug 2026). Specializes constrained decoding for **finite-set / enum** constraints (tool registries, label taxonomies, Semantic-ID allowlists) instead of compiling them through general CFG/FSM pipelines. Character-level trie + Aho-Corasick BPE alignment precomputes per-node token masks; decode is a cached lookup. Paper claims: 7x faster per-step mask vs XGrammar (0.65 us vs 5.8 us), flat sub-100 ms compile to K=10k, and **29x** end-to-end vLLM throughput at batch 256 via a **stateless LogitsProcessor** path that bypasses guided-decoding scheduling. Formal output-equivalence to FSM (Proposition 1). Implementation described as Rust + PyO3 (`aho-corasick` 1.1). Explicitly complementary to **STATIC** (Su et al. 2602.22647, already catalogued) and to LLGuidance (startup vs per-step tradeoff).

**Revvel hit:** when `deliver:*` or tool routing must pick from **hundreds-tens of thousands** of sealed strings (label graphs, ticket IDs, MCP tool names) and XGrammar/provider enum limits wall out, this is the metal paper to watch for a production vLLM drop-in. Keep **static-constraint-decoding** for the archived accelerator kernels; keep **xgrammar-2** / **llguidance** for full CFG / JSON Schema. Do **not** treat as a CFG replacement for `wr:code` grammars.

**Honesty:** WATCH. Verified 2026-09-25 (America/Denver): arXiv abs + pdf **200** (last-modified Aug 2026). Paper conclusion: *"code will be released upon publication"* -- **no public GitHub / PyPI / crates.io artifact found this pass**. License unknown until release. Stars/N/A. Re-check every scrape for the code drop; until then do not wire into revvel-standards.

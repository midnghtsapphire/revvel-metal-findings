# cbdl

```json
{
  "id": "cbdl",
  "name": "CBDL: constrained beam decoding with lookup for valid imports in generated tests",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.41878"
  ],
  "license": "arXiv paper (no code found)",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "Constrained decoding applied to the part of wr:code test generation that fails most mechanically: imports. Guarantees 100% valid imports (Python/Java), avoids the import-streak degeneration plain grammar masks cause, and a small local model with CBDL writing imports + a frontier model writing the body beat the frontier model alone. Self-hosted path only; paper only.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-02"
}
```

**No More Import Errors: Constrained Decoding for Guaranteed Valid Imports in LLM-Generated Tests** (Kitsios, Biagiola, Salvaneschi, Bacchelli). arXiv **2610.41878** v1, submitted 2026-10-30 09:26 MDT (cs.SE).

Import errors are among the most common failures of LLM test generation. A plain grammar mask over valid imports can degenerate into **import streaks** (repeating valid imports until the token budget runs out). **CBDL** (Constrained Beam Decoding with Lookup) keeps the validity guarantee while avoiding premature commitment to tokens that lead to such streaks. Authors' numbers (Python and Java, two test-generation tasks): **100% valid imports**, vs 45% / 10% / 43% of import errors left unresolved by RAG, LIBRO and agentic repair; +1-4 pp test correctness over unconstrained generation; +2-7 pp (Python) / +1-6 pp (Java) when combined with agentic repair; a hybrid where a small local model with CBDL writes the imports and GPT-5.2 writes the test body beats GPT-5.2 alone by 1-3 pp. Overhead 16-21 s per test.

**Revvel hit:** adds a concrete, narrow use for the mask engines in lane 01 (**xgrammar-2**, **llguidance**, **glrmask**): constrain only the imports of tests the coder writes, against the repo's real module index, and leave the body free. Also a warning for any grammar mask revvel uses: a valid-only mask can still loop, so cap or look ahead. Only applies if a local model is in the loop; OpenRouter path unaffected.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-02 (America/Denver): arXiv abs 200, export API metadata and abstract read. No code link found in the abstract or PDF. Results are the authors' own.

# ChopChop

```json
{
  "id": "chopchop",
  "name": "ChopChop (semantic constrained decoding)",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://doi.org/10.1145/3776708",
    "https://arxiv.org/abs/2509.00360",
    "https://github.com/large-loris-models/chopchop",
    "https://popl26.sigplan.org/details/POPL-2026-popl-research-papers/68/ChopChop-A-Programmable-Framework-for-Semantically-Constraining-the-Output-of-Langua"
  ],
  "license": "MIT",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "wr:code on TS: programmable AST pruners (type safety / equivalence) beyond CFG masks — gate openrouter-coder emit before spec-approved",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-15"
}
```

Nagy, Zhou, Polikarpova, D'Antoni — PACMPL / POPL 2026. First programmable framework for **semantic** constrained decoding: users write pruners over AST-like `TreeGrammar` spaces; coinductive realizability decides whether a prefix can still complete into a constraint-satisfying program. Demonstrated on (1) TypeScript type safety and (2) equivalence to a reference program (e-graphs). Paper + MIT GitHub verified 2026-09-15.

**Revvel hit:** XGrammar / LLGuidance / GBNF cage syntax. Type-constrained PLDI cages types. ChopChop is the next layer — user-defined semantic pruners so a `wr:code` patch that cannot typecheck or cannot match a reference rewrite never leaves the coder. Map onto the existing coder contract; do not stand up a second decode pipeline.

**Honesty:** CAN-PARTIAL. Artifact + arXiv + ACM DOI live. Research prototype (Python 3.12+, Lark grammars); not a drop-in for vLLM/OpenRouter yet.

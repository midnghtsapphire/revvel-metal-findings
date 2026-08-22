# Type-constrained code generation (PLDI 2025)

```json
{
  "id": "type-constrained-codegen-pldi-2025",
  "name": "Type-Constrained Code Generation with Language Models",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://doi.org/10.1145/3729274",
    "https://arxiv.org/abs/2504.09246",
    "https://pldi25.sigplan.org/details/pldi-2025-papers/25/Type-Constrained-Code-Generation-with-Language-Models"
  ],
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "wr:code on TS/JS: type-safe decode or post-mask so spec-approved interfaces compile before auto-merge",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Mündler et al., PACMPL / PLDI 2025. Prefix automata + inhabitable-type search. Reported: TS compile errors down more than 50%; repair +37% relative. HTML arXiv conversion failed this scrape; use abs + DOI.

**Revvel hit:** the SSOT is JavaScript. CircleCI + `wr-lint` already exist. A type mask on `openrouter-coder` output is the paper's method applied to #15507: the patch that cannot typecheck cannot be the handoff.

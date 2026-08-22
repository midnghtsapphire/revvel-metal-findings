# Correctness-guaranteed constrained decode (COLM 2025)

```json
{
  "id": "colm-2025-correctness-guaranteed-decode",
  "name": "Correctness-guaranteed constrained decoding (COLM 2025)",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://openreview.net/forum?id=CYiXNIQegF",
    "https://arxiv.org/pdf/2508.15866"
  ],
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "OUTPUT_TYPE + MCP/API products: grammar = public API, not chat. Steal the method, not sLua.",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Tree-of-Parsers + non-extensible regexes. Semantic / API-correct sLua in a game trial. Runtime guarantees on the accepted language.

**Revvel hit:** `standards/shapes/*.md` already name the public shape. This paper is the argument that the grammar *is* the product contract. Adopt the method for MCP/API `OUTPUT_TYPE`s.

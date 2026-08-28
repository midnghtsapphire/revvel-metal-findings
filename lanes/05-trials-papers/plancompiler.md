# PlanCompiler

```json
{
  "id": "plancompiler",
  "name": "PlanCompiler",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2604.13092",
    "https://github.com/prnvh/plancompiler",
    "https://github.com/prnvh/plancompiler/releases/tag/v1.1.0"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "spec-approved as 7 static checks over a closed primitive registry before any coder emit",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-28"
}
```

LLM may only pick nodes from a 25-node typed registry and bind required params. Seven deterministic checks (existence, edges, types, acyclicity, orphans, arity, required params) abort before compile. Compiler assembles pre-written templates; no second LLM call. Paper + v1.1.0: 278/300 first-pass vs 202/300 GPT-4.1. Residual failures: QueryEngine SQL evasion (open surface) and DBHandle type confusion (validator catches). github.io writeup 404 this scrape; arxiv + repo + tag live.

**Revvel hit:** treat `schemas/` + label gates as the registry. `spec-approved` is CHECK 1–7. Do not import the pandas node library. If a WR names a primitive that is not in `standards/shapes`, reject it the same way CHECK 1 rejects an unknown node.

**Honesty:** CAN-PARTIAL. Architecture is the lesson. Closed data-pipeline registry is not the WR surface.

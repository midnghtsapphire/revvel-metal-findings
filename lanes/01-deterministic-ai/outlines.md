# Outlines

```json
{
  "id": "outlines",
  "name": "Outlines",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/dottxt-ai/outlines",
    "https://arxiv.org/abs/2307.09702"
  ],
  "license": "UNKNOWN (LICENSE body empty on fetch)",
  "metal": 3,
  "determinism": 4,
  "revvel_hit": "research-engine.js extractors: Pydantic/JSON Schema before a WR PR is opened",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22"
}
```

Python structured generation. Pydantic / JSON Schema / regex / CFG on transformers, llama.cpp, vLLM, Ollama, OpenAI-class APIs. Paper: arXiv 2307.09702.

**Revvel hit:** `scripts/research-engine.js` dumps become schema-valid (`Decision ∈ {BUILD,HOLD,ARCHIVE}`, `research_mode`, viability 1–5) *before* `wr-pr-creation.yml`. That stops garbage packets from becoming essays.

**Honesty:** SPDX not verified this scrape. Treat as Python glue over a real mask engine, not as the engine itself.

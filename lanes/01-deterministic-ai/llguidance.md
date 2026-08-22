# LLGuidance

```json
{
  "id": "llguidance",
  "name": "LLGuidance",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/guidance-ai/llguidance",
    "https://guidance-ai.github.io/llguidance/llg-go-brrr"
  ],
  "license": "UNKNOWN (Microsoft CLA on repo; SPDX not opened this scrape)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Cage Project v2 / OUTPUT_TYPE / MCP tool JSON so OpenRouter cannot emit illegal fields",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

v1.0.0 (2025-06-23). CFG / JSON Schema constrained decoder. Claimed ~50µs/token on their blog. Shipped in OpenAI Structured Outputs, vLLM, SGLang, llama.cpp, Chromium.

Same automaton idea as XGrammar and GBNF, closer to the serving path Revvel already pays for (OpenRouter → OpenAI-class structured outputs).

**Revvel hit:** bind `OUTPUT_TYPE` enums, viability-gate JSON, MCP tool schemas. Structure is the determinism lever. `temperature=0` + `seed` is best-effort (OpenAI `system_fingerprint` can still diverge).

**Vs XGrammar / GBNF:** use LLGuidance when the call already goes through a vendor structured-output API. Keep GBNF for local llama.cpp. Do not stack three masks on one request.

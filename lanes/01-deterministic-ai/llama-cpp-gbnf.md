# llama.cpp GBNF

```json
{
  "id": "llama-cpp-gbnf",
  "name": "llama.cpp GBNF / JSON Schema → grammar",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/ggml-org/llama.cpp/blob/master/grammars/README.md",
    "https://github.com/ggml-org/llama.cpp"
  ],
  "license": "MIT (llama.cpp)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Offline twin of XGrammar for schemas/*.json — no OpenRouter structured-output dependency",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

GGML BNF. Formal grammar applied during sampling. Invalid tokens get logit `-inf`. CLI `--grammar` / `--grammar-file`; server `grammar` body field; JSON Schema subset via `--json` / `json_schema` / `response_format`. Converter: `examples/json_schema_to_grammar.py`. Validator: `tests/test-gbnf-validator.cpp`. Optional LLGuidance path (`LLAMA_LLGUIDANCE=ON`) for heavier structured output.

Schema is **not** injected into the prompt unless you are in tool-calling. Describe the shape in the prompt too, or the model is flying blind inside a cage.

**Revvel hit:** `schemas/state.schema.json` and WR packet schemas should have a checked-in `.gbnf`. Local coder / research-engine can run without a vendor JSON mode. XGrammar stays the cloud/vLLM path. GBNF is the air-gapped twin. Same automaton idea, closer to C.

**Caveat:** JSON Schema support is a subset. Regex lookaheads and some Draft features are skipped. Write a schema-specific grammar, not generic `json.gbnf`, or keys can still drift inside valid JSON.

**Next trial:** convert `schemas/state.schema.json` with `json_schema_to_grammar.py`, generate 50 packets with `llama-cli --json`, assert 50/50 parse. Receipt or it did not happen.

# XGrammar-2

```json
{
  "id": "xgrammar-2",
  "name": "XGrammar-2",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/mlc-ai/xgrammar/",
    "https://blog.mlc.ai/2026/05/04/xgrammar-2-fast-customizable-structured-generation",
    "https://arxiv.org/html/2601.04426v2",
    "https://doi.org/10.1145/3786335.3813124"
  ],
  "license": "Apache-2.0 (confirm on repo)",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": ".github/workflows/openrouter-coder.yml + schemas/ — grammar-mask coder output",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Constrained decoding engine. Compiles a CFG / JSON Schema / structural tag into a token mask. Invalid tokens get probability 0. XGrammar-2 (May 2026) adds TagDispatch and cross-grammar cache for agentic, mid-request structure changes. Default structured-gen backend in vLLM, SGLang, TensorRT-LLM, MLC-LLM. Paper: ACM Conference on AI and Agentic Systems 2026.

This is the closest thing to machine language on the *generation* side: the automaton sits on the logits.

**Revvel hit:** `openrouter-coder.yml` currently hopes the model emits a usable patch. Bind it to `schemas/` (WR packet, state, deliver matrix). Malformed coder output should be physically impossible. That is how you stop WR essays and start `wr:code`.

**Caveat:** temperature=0 + grammar ≠ bit-identical across GPUs/kernels. Structure is deterministic. Token choice among legal tokens is not always.

**Next trial:** take `schemas/state.schema.json` from revvel-standards, compile it with XGrammar or an OpenRouter/vLLM structured-output path, generate 50 packets, assert 50/50 parse.

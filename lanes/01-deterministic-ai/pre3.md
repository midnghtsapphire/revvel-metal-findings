# Pre³ — Deterministic PDA Structured Decoding (LightLLM)

```json
{
  "id": "pre3",
  "name": "Pre³ (DPDA constrained decoding)",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2506.03887",
    "https://aclanthology.org/2025.acl-long.551/",
    "https://github.com/ModelTC/LightLLM",
    "https://www.light-ai.top/lightllm-blog/2025/06/15/pre3.html"
  ],
  "license": "Apache-2.0 (LightLLM)",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Cage Project v2 / openrouter-coder structured JSON — LightLLM self-host mask path beside XGrammar",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-16"
}
```

ACL 2025 Outstanding Paper. Transforms LR(1) grammars into a **deterministic pushdown automaton** via prefix-conditioned edges so constrained decoding does table lookup instead of runtime PDA exploration. Claims up to **~40% lower TPOT** and **~36% higher throughput** vs prior structured engines; beats XGrammar on large-batch LightLLM serving in their evals.

Shipped inside **ModelTC/LightLLM** (~2k Python + ~1k C++). Not a vLLM drop-in — only matters if you self-host LightLLM (or port the DPDA tables).

**Revvel hit:** keep LLGuidance / XGrammar on the vendor and vLLM paths you already pay for. Watch Pre³ when a self-hosted LightLLM coder must emit schema-valid `wr:code` / WR dumps at batch. Do not invent a second pipeline — swap the mask engine behind the existing coder contract.

**Honesty:** paper + LightLLM repo + blog verified live this scrape. Production OpenRouter path not claimed.

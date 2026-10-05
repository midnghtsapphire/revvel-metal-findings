# PSC — Parser Stack Classification

```json
{
  "id": "psc",
  "name": "PSC (Parser Stack Classification)",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2608.03065",
    "https://dl.acm.org/doi/10.1145/3832172",
    "https://openreview.net/forum?id=SEjxNfQTHN",
    "https://github.com/Gompyn/PSC"
  ],
  "license": "UNKNOWN (paper + open-source replication; SPDX not opened this scrape)",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Cage Project v2 / openrouter-coder structured JSON — next mask engine after LLGuidance when self-hosting",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-27"
}
```

Peer-reviewed: published 2026-10-01 in Proceedings of the ACM on Software Engineering, Vol. 3, ISSTA issue (DOI 10.1145/3832172; Li, Dong, Li, Li). Earlier ICLR 2026 submission. Precomputes FSAs over parser stacks so mask compute is **O(stack)** and independent of vocabulary size. Claims up to **~700×** faster mask compute than LLGuidance on Java/Go/SQL grammars, ~30× on JSON Schema; end-to-end throughput approaches unconstrained.

Python ~1100 LOC; uses Lark LALR(1). Preprocessing for JSON schemas is cheap (~30s); programming-language grammars can take minutes–hours and large RAM (SQL ~250 GiB in paper).

**Revvel hit:** keep LLGuidance on the OpenRouter / vendor structured-output path you already pay for. Watch PSC for any self-hosted vLLM/SGLang coder that must emit `wr:code` / schema-valid WR dumps without mask tax. Do not invent a second pipeline — swap the mask engine behind the existing coder contract.

**Honesty:** paper + replication package verified live; ACM DOI page confirmed via search index 2026-10-05 (direct curl gets 403 bot-block from dl.acm.org). Replication repo (Gompyn/PSC) still a research/bench harness (`fast_constraint` + `benchmark/src/vllm_inference.py`), not a packaged vLLM plugin. Production drop-in for OpenRouter not claimed.

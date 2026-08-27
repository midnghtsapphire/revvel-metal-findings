# PSC — Parser Stack Classification

```json
{
  "id": "psc",
  "name": "PSC (Parser Stack Classification)",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2608.03065",
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

ICLR 2026 submission. Precomputes FSAs over parser stacks so mask compute is **O(stack)** and independent of vocabulary size. Claims up to **~700×** faster mask compute than LLGuidance on Java/Go/SQL grammars, ~30× on JSON Schema; end-to-end throughput approaches unconstrained.

Python ~1100 LOC; uses Lark LALR(1). Preprocessing for JSON schemas is cheap (~30s); programming-language grammars can take minutes–hours and large RAM (SQL ~250 GiB in paper).

**Revvel hit:** keep LLGuidance on the OpenRouter / vendor structured-output path you already pay for. Watch PSC for any self-hosted vLLM/SGLang coder that must emit `wr:code` / schema-valid WR dumps without mask tax. Do not invent a second pipeline — swap the mask engine behind the existing coder contract.

**Honesty:** paper + replication package verified live. Production drop-in for OpenRouter not claimed.

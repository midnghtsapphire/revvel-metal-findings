# deepinfer

```json
{
  "id": "deepinfer",
  "name": "DeepSeek DeepInfer",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/deepseek-ai/DeepInfer",
    "https://github.com/deepseek-ai/deepseek-recipe"
  ],
  "license": "Apache-2.0",
  "metal": 4,
  "determinism": 4,
  "revvel_hit": "second production engine shipping batch-invariant inference + deterministic sampling + regex/JSON-Schema/EBNF structured outputs in one switch set; evidence that bit-reproducible self-hosted coder output is a vendor feature now, not research",
  "honesty": "CANNOT",
  "acquired": "2026-10-21"
}
```

**DeepInfer** -- DeepSeek's in-house inference framework behind its V4.1-Flash production service, open-sourced 2026-10-20 (repo created 2026-10-16 01:47 MDT, last push 2026-10-20 22:55 MDT, ~17k★, Apache-2.0). Kernels: FlashMLA, DeepGEMM, DeepEP, TileKernels, DeepSelect, custom TileLang. Companion `deepseek-recipe` (MIT) encodes Chat Completions / Messages / Responses requests the way the official API does.

Determinism switches from the README:

- **Batch-invariant inference:** `DEEPINFER_BATCH_INVARIANT=1` (NVIDIA only).
- **Deterministic sampling:** `DEEPINFER_BATCH_INVARIANT=1 DEEPINFER_ENABLE_MTP_VARLEN=0` plus a fixed `seq_seed` in `SamplingParams` (NVIDIA only). Speculative decoding (DSpark, MTP varlen) must be off for it.
- **Structured outputs:** regex, JSON Schema or EBNF via `so_args={"schema_type": ..., "schema": ...}`.

**Revvel hit:** not usable today. It serves one model (DeepSeek-V4.1-Flash) on NVIDIA SM100 or Huawei Ascend 950 only, with no KV-cache system, P/D disaggregation or load balancing in the release. Useful as a reference: the exact flag set (batch invariance + no speculative varlen + fixed per-sequence seed) is the recipe any self-hosted replay of the coder needs, and the same shape as **vllm-batch-invariance**. Qualify with **vosti**'s 4-axis logit test before trusting it.

**Honesty:** CANNOT (for now), watching. Verified 2026-10-21 (America/Denver): repo API (Apache-2.0, not fork/archived), README read raw (determinism lines, hardware list, license). News coverage at https://aicoder.com/news/news-20261020-deepseek-deepinfer-open-source-inference-framework (200). Vendor throughput charts only, no head-to-head numbers. Not run.

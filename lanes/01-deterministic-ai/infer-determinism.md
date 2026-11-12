# infer-determinism

```json
{
  "id": "infer-determinism",
  "name": "infer-determinism: kernel-level batch-invariance probe harness",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/JonSnow1807/infer-determinism"
  ],
  "license": "MIT",
  "metal": 5,
  "determinism": 5,
  "revvel_hit": "Self-hosted coder only: a ready harness that proves (raw-bit comparison, per-record reproducer) whether vLLM batch-invariant mode, FlashAttention, FlashInfer and Triton autotune configs really give the same bits regardless of batch. Three H100 runs published: vLLM FlashAttention num_splits=1 and FlashInfer decode with disable_split_kv invariant; spec decoding (n-gram, EAGLE3) invariant under VLLM_BATCH_INVARIANT=1; one Hopper Triton pipelined-wgmma race (vllm#65385 chunk_scaled_dot_kkt) with a 15-line repro. Would be the acceptance test before trusting detent / vllm-batch-invariance. Watch-only while revvel-standards uses OpenRouter.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-12"
}
```

**infer-determinism** (`JonSnow1807/infer-determinism`, MIT, created 2026-11-06, pushed 2026-11-09). Runs a probe request alone, then repeats it while varying batch size, probe position, companion KV length, tile boundary, split setting or CUDA-graph replay, and compares raw floating-point bits (plus changed-element count, max abs diff, max ULP). `repro RECORD_ID` emits a standalone script for any divergence; `sweep` replays every Triton autotune launch per config. Skips are explicit and never counted as passes.

**Revvel hit:** if a coder is ever self-hosted, run `python -m infer_determinism run --quick` on the serving box as the gate before claiming batch-invariant output. Pairs with detent, vllm-batch-invariance and sfu-sim. No new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-12 (America/Denver): GitHub API (MIT, 0 stars, not archived); README read including the three H100 run summaries. Not run; results are the author's on one GPU.

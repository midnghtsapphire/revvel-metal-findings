# vllm-batch-invariance

```json
{
  "id": "vllm-batch-invariance",
  "name": "vLLM batch invariance (VLLM_BATCH_INVARIANT=1)",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://docs.vllm.ai/en/stable/features/batch_invariance/",
    "https://docs.vllm.ai/en/v0.31.0/features/batch_invariance/",
    "https://github.com/vllm-project/vllm/issues/27433",
    "https://github.com/vllm-project/vllm/issues/39096",
    "https://github.com/vllm-project/vllm/pull/52231",
    "https://vllm.ai/blog/2026-10-14-train-inference-consistency"
  ],
  "license": "Apache-2.0",
  "metal": 4,
  "determinism": 4,
  "revvel_hit": "Self-hosted coder path only: `VLLM_BATCH_INVARIANT=1 vllm serve …` + fixed `seed` makes the same wr:code request produce the same tokens regardless of batch size/order, so a chronicle/agentape replay can be re-run live and diffed instead of trusting the cassette alone. Closes the `temperature=0 + seed is best-effort` caveat in xgrammar-2 / llguidance for the box you own; OpenRouter path unaffected",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-13"
}
```

**vLLM batch invariance** -- an env-var mode in vLLM (`VLLM_BATCH_INVARIANT=1`, set before import or on `vllm serve`) that switches to deterministic kernel implementations for attention and other ops, keeps numerics consistent across batch sizes, and disables optimizations that add non-determinism (e.g. custom all-reduce under tensor parallelism). Result per the docs: output is deterministic and independent of batch size or the order of requests in the batch, including sampled (`temperature>0`) requests with a fixed `seed`. Hardware: NVIDIA compute capability ≥ 8.0, or Intel XPU with the Triton attention backend. **AMD ROCm (gfx90a / gfx942 / gfx950) merged on `main`** in PR #52231 (2026-10-12 09:53 MDT, merge `e0317b28ce3b`): before it, the flag was set on ROCm but ordinary kernels ran and the determinism suite skipped itself; the PR makes the mode real there and mirrors the NVIDIA batch-invariance CI steps on MI250 / MI300 / MI355. Not in a release yet (latest vLLM is still v0.31.0, 2026-10-05). Tested-model list in the docs covers DeepSeek V3/R1, Qwen3 dense/MoE/VL, and others. Performance cost is intentional. Documented on the v0.31.0 docs (current release, 2026-10-05).

**Revvel hit:** fits the existing replay lane, no new pipeline. When a wr:code run on a self-hosted vLLM coder goes wrong, the cassette (**chronicle** / **agentape**) records what happened. With batch invariance on, the same request re-run against the same weights should reproduce it token-for-token, which turns "flaky model" into a diffable regression. Combine with the grammar mask (**xgrammar-2**; vLLM 0.31.0 pins `xgrammar == 0.2.7`) for structure + reproducibility. Does nothing for OpenRouter / vendor calls.

**2026-10-14 vLLM blog ("Finish RL Training Faster: Bitwise-Consistent…"):** the vLLM team treats the inference kernels as the numerical reference and removes shape-based kernel switches in batch-invariant mode (e.g. FP8 linear always on DeepGEMM, one FP32-output router GEMM at every batch size, fixed-order Triton kernel for small BF16 matmuls). Signals the mode is being hardened for production RL, not just a demo. A separate DeepSeek-V4 batch-invariant kernel PR (#54955) is an open preview marked DO NOT MERGE.

**Honesty:** CAN-PARTIAL. Rechecked 2026-10-16 (America/Denver): PR #52231 merged (GitHub API); blog post and PR #54955 pages 200 (summarised from search extracts, not read in full); #27433 still open (last updated 2026-10-14 01:00 MDT); #39096 still open (last updated 2026-08-16); PyPI vllm still 0.31.0. Verified 2026-10-13 (America/Denver): docs pages (stable + v0.31.0) 200 and read. Still marked **beta**; tracking issue #27433 open (last updated 2026-10-09). Known hole: issue #39096 (open) reports batch invariance breaking on SM<90 GPUs (Ampere/Ada) under `torch.compile` and/or CUDA graphs, which are on by default; the repo's own tests force eager mode there. Run on Hopper+ or with `enforce_eager=True`, and assert reproducibility in CI before relying on it. Interaction with structured-output masks was not separately verified. Watching until beta is lifted or #39096 is fixed; the ROCm path becomes usable for a self-hosted coder once the release after v0.31.0 ships.

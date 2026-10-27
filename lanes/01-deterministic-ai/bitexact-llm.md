# bitexact-llm

```json
{
  "id": "bitexact-llm",
  "name": "BitExact LLM (integer Llama inference)",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/mynotwo/bitexact-llm",
    "https://github.com/mynotwo/bitexact-llm/releases/tag/v0.1.0-repro-preview",
    "https://mynotwo.github.io/blog/bitexact-inference/",
    "https://github.com/mynotwo/bitexact-llm/tree/main/experiments/rl_mismatch"
  ],
  "license": "Apache-2.0",
  "metal": 5,
  "determinism": 5,
  "revvel_hit": "Reference for the step after batch invariance: integer (fixed-point) inference gives the same int64 logits and sampled tokens across GPUs, CPUs and batch/KV schedules, so a replay record could carry a logits hash that any machine can re-check. One small model (Llama-3.2-1B), research prototype; borrow the record/compare report shape, do not adopt as the coder engine.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-26",
  "updated": "2026-10-27"
}
```

**BitExact LLM** -- Yu Mao's personal research project: an experimental Llama-3.2-1B inference engine built on integer arithmetic. Repo created 2026-10-23 14:44 MDT, last push 2026-10-25 23:22 MDT, Apache-2.0 (LICENSE file present), 1★. One GitHub pre-release, `v0.1.0-repro-preview` (2026-10-25 23:22 MDT). Not on PyPI. Write-up: "Cross-hardware bitwise reproducibility in LLM inference" (blog dated 2026-10-23).

How it works (README): every tensor on the forward and sampling path is an integer with a fixed number of fractional bits, and every rounding is an integer rule. Integer addition is associative, so summation order (tile size, split-K, batch, hardware) cannot change the result. Matrix products split activations and bf16 weights into int8 limbs on int8 tensor cores with int32 accumulators that cannot overflow, joined in int64; RMSNorm, RoPE, softmax and SiLU use integer maths and precomputed tables; sampling uses integer Gumbel noise keyed by (seed, token index).

- **exact mode**: original bf16 weights (input embedding is the one stated exception), int64 fixed-point activations; logits within ~5e-5 of HF fp32.
- **int8 mode**: quantized integer model; ~9e-2 from fp32. Served through an **optional vLLM 0.32.0 plugin** (paged integer attention on vLLM's own KV cache, prefix cache, CUDA graphs).
- **Reported identity:** 0 differing tokens and 0 differing logits hashes over 3,696 positions across batch 1/8, incremental decode and torch.compile on two H800s, an H100, an x86 CPU and an Apple M4 Pro CPU; the vLLM plugin matched the standalone engine over 14 runs (chunked prefill, prefix cache on/off, preemptions, contexts up to 14,000 tokens).
- **CPU self-check without weights:** `python -m bitexact.repro self-check --out arithmetic.json` checks eight arithmetic fixtures against Python references; `examples/check_bit_identity.py record|compare` produces and compares per-device reports.

**Revvel hit:** the coder runs on hosted models, so this cannot be adopted for wr:code output. What transfers is the *report shape*: record a per-position logits/token hash on one machine and compare it on another, with a stated scope. That is the same check **vosti**'s 4-axis logit test and **vllm-batch-invariance** need for any self-hosted replay, and it extends them from "same build, any batch" to "any device". Keep watching; no new pipeline.

**Honesty:** CAN-PARTIAL. Verified 2026-10-26 (America/Denver): GitHub repo + releases API (created/pushed dates, Apache-2.0, pre-release tag), raw LICENSE (Apache License 2.0) and README, blog page 200. Not run. Limits the README states itself: reproducibility not speed (vLLM plugin ~0.28x stock vLLM bf16 throughput at batch 32; exact prefill ~20x slower); the historical model runs predate newer overflow guards and the changed source still needs a fresh CUDA reproduction; bound checks "are not a proof that every arithmetic operation is overflow-free"; plugin is single-GPU, temperature+seed sampling only (top-k/top-p ignored), offline `LLM` API only (not `vllm serve`), cross-GPU tests sm90 only. Single-author, three days old.

**Update 2026-10-27 -- replay experiment (no new release).** Commits on main 2026-10-26 → 10-27 (PR #4, `experiments/rl_mismatch/`; #3 README clarification); latest release still `v0.1.0-repro-preview`. On Llama-3.2-1B / 128 GSM8K prompts, re-sampling grader-flagged failures with the same prompts and seeds reproduced token-for-token only **13–17%** of them on stock vLLM 0.32.0 bf16 (median first divergence ~50–64 tokens; 4–10 verdicts flipped to correct), versus **1,007 / 1,007** with BitExact across H800, H100, batch/order changes and the standalone engine (15/15 on x86 CPU). Sampler vs scorer log-prob mismatch was 0 for BitExact (SHA-256 of int64 logits rows identical). Caveat the README states: float64 log-softmax differed across numpy 1.26 vs 2.3.5 (6.5% of values, up to 7.1e-15), so compare **integer logits**, not derived log-probs. Inference only, one model, one task.

**Revvel hit (2026-10-27):** concrete evidence for why a replay record should hash raw integer/logit outputs rather than decoded probabilities, and that "same seed" replay on a stock engine is not reproduction. Still watching; borrow the report shape only.

**Honesty (2026-10-27):** CAN-PARTIAL. Verified 2026-10-27 (America/Denver): GitHub contents API for `experiments/rl_mismatch/`, raw README read, tree page 200, releases unchanged. Numbers are the author's; not reproduced.

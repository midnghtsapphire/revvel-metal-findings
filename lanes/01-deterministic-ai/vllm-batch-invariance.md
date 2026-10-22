# vllm-batch-invariance

```json
{
  "id": "vllm-batch-invariance",
  "name": "vLLM batch invariance (VLLM_BATCH_INVARIANT=1)",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://docs.vllm.ai/en/stable/features/batch_invariance/",
    "https://docs.vllm.ai/en/v0.32.0/features/batch_invariance/",
    "https://github.com/vllm-project/vllm/issues/27433",
    "https://github.com/vllm-project/vllm/issues/39096",
    "https://github.com/vllm-project/vllm/pull/52231",
    "https://vllm.ai/blog/2026-10-14-train-inference-consistency",
    "https://github.com/vllm-project/vllm/releases/tag/v0.32.0",
    "https://arxiv.org/abs/2609.38981",
    "https://github.com/vllm-project/vllm/issues/59086",
    "https://github.com/vllm-project/vllm/pull/60479"
  ],
  "license": "Apache-2.0",
  "metal": 4,
  "determinism": 4,
  "revvel_hit": "Self-hosted coder path only: `VLLM_BATCH_INVARIANT=1 vllm serve …` + fixed `seed` aims to make the same wr:code request produce the same tokens regardless of batch size/order, so a chronicle/agentape replay can be re-run live and diffed instead of trusting the cassette alone. Released for NVIDIA SM>=8.0, AMD Instinct (gfx90a/942/950) and Intel XPU in vLLM 0.32.0. Qualify it on your model first: Vosti's tests found logit mismatches in the batch-invariant mode on Gemma3-4B (Llama3.1-8B matched). OpenRouter path unaffected",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-13",
  "updated": "2026-10-20"
}
```

**vLLM batch invariance** -- an env-var mode in vLLM (`VLLM_BATCH_INVARIANT=1`, set before import or on `vllm serve`) that switches to deterministic kernel implementations for attention and other ops, keeps numerics consistent across batch sizes, and disables optimizations that add non-determinism (e.g. custom all-reduce under tensor parallelism). Result per the docs: output is deterministic and independent of batch size or the order of requests in the batch, including sampled (`temperature>0`) requests with a fixed `seed`. Hardware: NVIDIA compute capability ≥ 8.0, or Intel XPU with the Triton attention backend. **AMD ROCm (gfx90a / gfx942 / gfx950) merged on `main`** in PR #52231 (2026-10-12 09:53 MDT, merge `e0317b28ce3b`): before it, the flag was set on ROCm but ordinary kernels ran and the determinism suite skipped itself; the PR makes the mode real there and mirrors the NVIDIA batch-invariance CI steps on MI250 / MI300 / MI355. Not in a release yet (latest vLLM is still v0.31.0, 2026-10-05). Tested-model list in the docs covers DeepSeek V3/R1, Qwen3 dense/MoE/VL, and others. Performance cost is intentional. Documented on the v0.31.0 docs (current release, 2026-10-05).

**Revvel hit:** fits the existing replay lane, no new pipeline. When a wr:code run on a self-hosted vLLM coder goes wrong, the cassette (**chronicle** / **agentape**) records what happened. With batch invariance on, the same request re-run against the same weights should reproduce it token-for-token, which turns "flaky model" into a diffable regression. Combine with the grammar mask (**xgrammar-2**; vLLM 0.31.0 pins `xgrammar == 0.2.7`) for structure + reproducibility. Does nothing for OpenRouter / vendor calls.

**2026-10-14 vLLM blog ("Finish RL Training Faster: Bitwise-Consistent…"):** the vLLM team treats the inference kernels as the numerical reference and removes shape-based kernel switches in batch-invariant mode (e.g. FP8 linear always on DeepGEMM, one FP32-output router GEMM at every batch size, fixed-order Triton kernel for small BF16 matmuls). Signals the mode is being hardened for production RL, not just a demo. A separate DeepSeek-V4 batch-invariant kernel PR (#54955) is an open preview marked DO NOT MERGE.

**Honesty:** CAN-PARTIAL. Rechecked 2026-10-16 (America/Denver): PR #52231 merged (GitHub API); blog post and PR #54955 pages 200 (summarised from search extracts, not read in full); #27433 still open (last updated 2026-10-14 01:00 MDT); #39096 still open (last updated 2026-08-16); PyPI vllm still 0.31.0. Verified 2026-10-13 (America/Denver): docs pages (stable + v0.31.0) 200 and read. Still marked **beta**; tracking issue #27433 open (last updated 2026-10-09). Known hole: issue #39096 (open) reports batch invariance breaking on SM<90 GPUs (Ampere/Ada) under `torch.compile` and/or CUDA graphs, which are on by default; the repo's own tests force eager mode there. Run on Hopper+ or with `enforce_eager=True`, and assert reproducibility in CI before relying on it. Interaction with structured-output masks was not separately verified. Watching until beta is lifted or #39096 is fixed; the ROCm path becomes usable for a self-hosted coder once the release after v0.31.0 ships.

**Update 2026-10-19 -- released in vLLM 0.32.0:** vLLM **v0.32.0** (GitHub release 2026-10-18 00:50 MDT; PyPI 04:03 MDT; Apache-2.0). Release notes, "Batch invariance": custom all-reduce under `VLLM_BATCH_INVARIANT=1` (#58623), deterministic split-K LoRA shrink (#59377), every attention backend checked for batch-invariance support (#60271), SM120 TP configs (#58495), and **ROCm support (#52231)**. The v0.32.0 docs page now lists hardware as NVIDIA CC >= 8.0, **AMD Instinct gfx90a / gfx942 / gfx950**, and Intel XPU with Triton. New implementation notes in the docs: under TP the 1-stage custom all-reduce is pinned with fixed-size chunking (FlashInfer/AITER/QuickReduce all-reduce disabled); on CUDA devices with tuned bf16 matmul table entries (Ada, Hopper, Blackwell) the mode runs **without `torch.compile`, using breakable CUDA graphs** (`VLLM_USE_BREAKABLE_CUDAGRAPH=0` to opt out); LoRA shrink split into 8 fixed K chunks. New warning: TP all-reduces whose size is not a multiple of 16 bytes can still switch between NCCL and custom all-reduce by batch size. Other 0.32.0 notes that touch a self-hosted coder: Python 3.10 dropped (3.11–3.14), `parallel_tool_calls=false` now enforced (#50502, #59298), xgrammar `propertyNames` (#57594), `requirements/common.txt` pins `xgrammar == 0.2.8` and `llguidance >= 1.7.0, < 1.8.0`.

Still **beta** (docs note unchanged). **#27433** (tracking) open, last updated 2026-10-14 01:00 MDT; **#39096** (SM<90 + torch.compile/CUDA graphs) open, last updated 2026-08-16. The new breakable-CUDA-graph path for Ada may be relevant to #39096 but the issue is not closed, so the hole is not treated as fixed.

**Independent check (new finding vosti, 05):** the Vosti paper (arXiv 2609.38981, 2026-09-30) measured vLLM **0.28.0** batch-invariant mode on one H200: on Llama3.1-8B both FA3 and Triton invariant backends matched every batch / chunked-prefill / prefill-decode / prefix-reuse logit comparison; on **Gemma3-4B every category had mismatches** (e.g. FA3 invariant: batch 193/296, chunk 0/90, prefill-decode 5/384). The authors call these scope limits, not necessarily bugs. Practical rule for revvel: before relying on live re-run determinism, run a batch + chunk + prefill-decode + prefix-reuse logit comparison on the exact model/backend you serve, in CI. That test is cheap compared with chasing a "flaky" wr:code diff.

**Status:** stays **watching** (beta, #39096 open, model-dependent per Vosti). Now a released, pinnable feature (`vllm==0.32.0`), so a trial on Hopper+ or AMD Instinct with the qualification test above is possible without building from `main`.

**Honesty (2026-10-19):** CAN-PARTIAL. Verified 2026-10-19 (America/Denver): PyPI JSON vllm 0.32.0; GitHub release v0.32.0 body read (batch-invariance and structured-output sections); v0.32.0 docs page fetched in full (200); `requirements/common.txt` at tag read; issues #27433 / #39096 and PRs #58623 / #60271 via API. Vosti numbers are from the arXiv HTML (read in full) and are for vLLM 0.28.0, not 0.32.0.

**Update 2026-10-20:** no vLLM release after **0.32.0** (PyPI). **#59086** ("`VLLM_BATCH_INVARIANT=1` is not batch-invariant for AWQ models on sm8x in the default mode") was **closed as completed 2026-10-20 07:33 MDT**, with no linked fix commit: the closing comment reports it no longer reproduces on `main` (nightly image `e68efc685ab1`, RTX 3090, `Qwen/Qwen3-8B-AWQ` compiled, no first-token diff and max |dlogprob| 0.0000 batched vs alone over three rounds; the commenter also closed their own fix PR #60013 as unneeded) and attributes the fix to #52231's override of the Inductor `.out` overloads for `mm`/`addmm` on SM80. Not verified against the 0.32.0 wheel itself. The sibling GPTQ fix **#60479** is still **open**. **#27433** and **#39096** still open; docs at v0.32.0 still say beta (200 via fetch; curl got 429 rate-limits). Status stays watching. Practical note: quantized (AWQ/GPTQ) self-hosted coders on Ampere are exactly where the per-model qualification test from **vosti** pays off.

**Honesty (2026-10-20):** verified 2026-10-20 (America/Denver): PyPI JSON, GitHub issues API (#59086 state/closed_at/timeline/comments, #39096), PR API (#60479 open), issue and PR pages 200, v0.32.0 docs page fetched.

**Update 2026-10-22:** still no vLLM release after **0.32.0** (PyPI). New open PR **#62365** (opened 2026-10-18 18:09 MDT, 38 commits): bitwise batch invariance for DeepSeek-V4.1-Flash under `VLLM_BATCH_INVARIANT=1` with CUDA graphs, DEP4, MTP and MegaMoE -- token ids and logprobs identical regardless of batch composition, chunk size, prefix-cache hit vs miss and DP rank; adds a BI CUDA op library (`csrc/batch_invariant/`) and opt-in faster `VLLM_BI_*` tiers that are batch invariant but round differently from the default path. Same model DeepInfer targets; unmerged. Separate field report (**concordance**, 2026-10-21): SGLang deterministic mode was 800/800 bit-stable, but the pipeline around it was not -- determinism of the server does not make the wr:code run reproducible by itself.

**Honesty (2026-10-22):** PR #62365 state via GitHub API (open, not merged) and PR description via search result; PyPI JSON vllm 0.32.0.

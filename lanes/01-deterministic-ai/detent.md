# detent

```json
{
  "id": "detent",
  "name": "Detent: Batch-Invariant LLM Serving and RL Rollouts at Near-Stock Speed",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.10611",
    "https://arxiv.org/html/2611.10611v1"
  ],
  "license": "n/a (paper; no code URL found on abs/HTML)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Self-hosted coder only (not OpenRouter): batch-invariant serving at 1.04-1.17x Stock latency per output token vs 1.67-10.3x for vLLM/SGLang deterministic modes (authors; Llama-3.1-70B, Qwen3-30B-A3B, multi-GPU). Fix only the few batch-dependent kernel-selection values instead of forcing one slow kernel per operator. Makes bit-exact wr:code replay affordable if the coder is ever self-hosted; pairs with vllm-batch-invariance / vosti checks. No code yet, so nothing to install.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-10"
}
```

**Detent** (Xin, Feng, Guo, Wu, Yin). arXiv **2611.10611** v1, submitted 2026-11-07. Engines pick each kernel and its parameters from the batch, so the same request can round differently depending on its batch neighbours. Deterministic modes fix that by keeping one conservative kernel per operator and pay 1.67-10.3x latency. Detent models kernel selection as a program, finds the fewest batch-dependent values that must be fixed, and tunes them per workload before deployment. Results (authors): batch-invariant on vLLM and SGLang across engines, GPU generations, TP degrees, dense and MoE; **1.04-1.17x** Stock latency per output token; matches SGLang deterministic-mode GSM8K accuracy; seeded RL rollouts up to Llama-3.1-70B replay bit for bit under other batches and cache splits; trainer logprobs match rollouts bit for bit at 1.03x Stock.

**Revvel hit:** the cost argument against bit-exact replay of wr:code runs goes away on a self-hosted coder. Today revvel-standards uses OpenRouter, so this is watch-only; if a self-hosted trial happens, Detent-style fixed selection values plus Vosti's four bitwise checks are the gate. Do not add a second serving pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-10 (America/Denver): arXiv export API abstract; abs (HTTP 200) and HTML v1 opened; only a DeepGEMM link in the HTML, no Detent code URL; GitHub repo search for Detent found nothing. Not run. Numbers are the authors'.

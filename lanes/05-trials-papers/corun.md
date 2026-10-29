# corun

```json
{
  "id": "corun",
  "name": "CoRun: Padding is Simple and Efficient for Deterministic LLM Inference",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2608.14376"
  ],
  "license": "arXiv paper (no code release found)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "If revvel-standards ever self-hosts the coder, deterministic output may not need slow batch-invariant kernels: schedule for position invariance (isolated prefill, fixed-shape decode) instead. Watch for code before trialling.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-29"
}
```

**CoRun: Padding is Simple and Efficient for Deterministic LLM Inference** (Shiju Zhao, Jiacheng Yang, Qihang Chen, Junhao Hu, Jiaqi Zheng, Guihai Chen, Xusheng Chen). arXiv **2608.14376** v1, submitted 2026-08-14 09:17 MDT (cs.OS / cs.PF); 13 pages.

Batch-dependent GPU execution (dynamic shapes change tiling and reduction order) is the main cause of run-to-run drift. Batch-invariant kernels fix it, but the authors report they cost more than 2x latency and up to 74% of serving throughput. CoRun's observation: most kernels are not batch-invariant but are **position-invariant**. So it gets determinism from **scheduling**: isolated prefill plus fixed-shape batched decode, run through CUDA graphs. On Qwen and DeepSeek models the authors report determinism with 15-324% higher throughput than batch-invariant approaches, 51.8% lower TTFT and 48.6% lower TPOT on average (authors' numbers).

**Revvel hit:** this is the runtime alternative to **vllm-batch-invariance**, **deepinfer** and **bitexact-llm** (01): if a self-hosted coder must be reproducible for replayed wr:code runs, CoRun suggests paying with padding rather than slow kernels. Only relevant if revvel-standards self-hosts inference. Pairs with **bi-acceptance-gates** (05).

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-29 (America/Denver): arXiv abs 200, export API metadata and abstract read. Older than the scrape window (August) but not tracked before. No code link found in the metadata. Not peer-reviewed; results are the authors' own; nothing run.

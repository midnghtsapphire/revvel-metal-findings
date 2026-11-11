# sfu-sim

```json
{
  "id": "sfu-sim",
  "name": "SFU-Sim: Bit-Exact Model of NVIDIA MUFU / PTX Special-Function Paths",
  "lane": "00-near-metal",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.13879",
    "https://arxiv.org/html/2611.13879v1",
    "https://github.com/hzX40000000/SFU-Sim"
  ],
  "license": "MIT",
  "metal": 5,
  "determinism": 5,
  "revvel_hit": "Self-hosted inference only: a CPU-side bit-exact reference for GPU special functions (ex2, lg2, rcp, rsqrt, sqrt, sin, cos, tanh; FP32/FP16/BF16/FP64-hi), exhaustively matched with zero mismatches on A100, Ada and Blackwell (authors' runs). Lets a determinism check explain softmax/activation drift across GPU generations without the GPU. Watch-only while revvel-standards uses OpenRouter.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-11"
}
```

**SFU-Sim** (arXiv **2611.13879** v1, submitted 2026-11-10; repo `hzX40000000/SFU-Sim`, MIT). Black-box reverse engineering of NVIDIA multi-function unit instructions, then the surrounding SASS for full PTX paths: 29 PTX paths (31 on sm_120 with BF16), every 32-bit (or 16-bit) input encoding compared against hardware, 0 mismatches. Computes each output directly, no lookup table or GPU needed; `make gpu-all` reruns the exhaustive comparison.

**Revvel hit:** if a coder is ever self-hosted, this is the reference for why the same kernel gives different bits on different GPU generations, next to detent / vllm-batch-invariance / vosti. Nothing to install today.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-11 (America/Denver): arXiv export API abstract; HTML v1 opened (links repo); GitHub API (MIT, created and pushed 2026-11-09); README read. Not run.

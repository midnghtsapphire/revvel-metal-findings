# vosti

```json
{
  "id": "vosti",
  "name": "Vosti: Specifying, Implementing, and Verifying Deterministic LLM Inference (QDelta/Vosti)",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2609.38981",
    "https://github.com/QDelta/Vosti"
  ],
  "license": "MIT",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Self-hosted coder path only, method first: copy Vosti's four determinism checks (batch composition, chunked-prefill budget, prefill vs decode, prefix-cache reuse; bitwise compare of full next-token logits) as a qualification test before any wr:code replay relies on a live re-run (vllm-batch-invariance). The engine itself is a single-GPU research prototype for dense Llama/Gemma/Qwen3 profiles; do not serve the coder on it. No second pipeline",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-19"
}
```

**Vosti** (Duke; arXiv **2609.38981**, submitted 2026-09-29 22:58 MDT) gives a system-level definition of deterministic LLM inference: for a fixed model and deployment configuration, two requests with the same prompt and initial sampler state must produce **bitwise-identical logits** (and so prefix-comparable token traces) at every output position both runs reach, whatever the batching, prompt chunking, prefill/decode path, or KV-cache reuse/eviction/recomputation. It then builds an engine verified against that definition:

- **Engine** in Rust, verified with **Verus**: an inductive proof that every engine step's logits depend only on the request's token history, carried by a KV-cache invariant (every live or retained reusable KV entry equals the value a cold forward over its exact token prefix would produce). Exact prefix matching (rolling hash only proposes; tokens, depth and parent page are checked), leaf-only eviction, and new KV written to private suffix slots.
- **Kernels** in a restricted, annotated Triton subset; a relational verifier lowers them to a tile IR and uses **Z3** to prove selected outputs are bitwise equal across batch layout, query length, prefill vs decode, and paged-KV layout. Kernel and tile configs are fixed per model + deployment; **a missing configuration is rejected at runtime instead of autotuned**.
- **Results (paper):** 5,488/5,488 bitwise matches across seven Llama/Gemma models on one H200. Measured against **vLLM 0.28.0** batch-invariant mode and **SGLang 0.5.19** deterministic mode: on Llama3.1-8B vLLM's invariant FA3 and Triton backends matched every comparison; on **Gemma3-4B all four production deterministic configurations had mismatches in every category** (e.g. vLLM invariant FA3 chunked-prefill 0/90). Decode throughput 1.36–3.19x vLLM's invariant modes; prefill slower; still slower than default modes and SGLang's deterministic modes.
- **Limits stated by the authors/README:** determinism only (not numerical correctness or progress); no equality across kernel plans, dtypes, compiler versions, or hardware; single GPU; dense text models only (README: Qwen3 dense, Gemma3 4B/12B/27B, Gemma4 12B/31B, Llama 3.1 8B / 3.2 3B / 3.3 70B); no MoE, multimodal, or linear attention; Triton compiler, translator, solver encoding, and the Rust/Python bridge are trusted.

**Repo:** `QDelta/Vosti`, MIT (`LICENSE`, "Copyright (c) 2026 Vosti contributors"), Rust, created 2026-09-29 11:35 MDT, last push 2026-09-30 20:11 MDT, 3★, no releases. README: research prototype and paper artifact; `make verify` (engine + kernel proofs) and `make test` run on CPU in the provided Docker image; GPU workflow builds a per-GPU deployment bundle.

**Revvel hit:** the useful part for revvel-standards is the **test**, not the engine. The replay lane assumes a self-hosted coder can be re-run and diffed; Vosti shows that assumption holds per model and backend, not globally. Before turning on live re-run diffs with **vllm-batch-invariance**, run the four comparisons on the exact model, backend, and vLLM version you serve, as a CI job on the existing workflow (point 5) -- if the box ever self-hosts. Watch the engine in case it grows a stable release or its kernel plans land upstream.

**Honesty:** CAN-PARTIAL. Verified 2026-10-19 (America/Denver): arXiv abstract page 200 and HTML read in full; arXiv API dates; GitHub API (MIT, not archived, no releases); README + LICENSE read raw. Not run (needs a GPU and model weights). Preprint, not peer-reviewed. The production-engine numbers are for vLLM 0.28.0 / SGLang 0.5.19 on H200 and two models; they do not describe vLLM 0.32.0.

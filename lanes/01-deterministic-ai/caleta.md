# caleta

```json
{
  "id": "caleta",
  "name": "Caleta: Evidence-Oriented Trust Layer for Reproducible Local LLM Inference",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.10324",
    "https://github.com/BiVelio/caleta",
    "https://github.com/BiVelio/caleta/tree/evidence-v1.1/experiments/real-gguf-qwen2.5-0.5b"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 4,
  "revvel_hit": "Pattern for scripts/local_llm.js (llama-cpp-gbnf path): versioned model manifest with exact size + SHA-256 checked before launch, llama-server bound to loopback with --offline, three-endpoint proxy, prompt-free execution records and JSON conformance reports. Borrow the manifest + verify-before-run step; do not adopt the Rust supervisor as a second runtime.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-10"
}
```

**Caleta** (Joan-Marc Fisa, BiVelio). arXiv **2611.10324** v1, submitted 2026-11-06. A Rust process supervisor and evidence layer around llama.cpp, not an inference engine. Combines versioned manifests, exact-size and SHA-256 artifact checks, controlled backend build, a restricted OpenAI-compatible proxy (`/health`, `/v1/models`, `/v1/chat/completions` only), prompt-free execution records, benchmark reports and a small conformance suite. Evaluated with 22 unit tests, deterministic end-to-end tests on Ubuntu/macOS/Windows, and one pinned real-model run (Qwen2.5-0.5B Q4_K_M, llama.cpp b11981, Windows CPU). The author is explicit that the measurements are descriptive, single-host, and not peer reviewed; open items are signed manifests, TOCTOU replacement, OS containment.

**Revvel hit:** the local fallback path (`scripts/local_llm.js` + `schemas/*.gbnf`) should refuse to start on a model file whose size/hash doesn't match a committed manifest, and should log a prompt-free record of model hash + backend build per run. That is a small step on the existing path, not a new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-10 (America/Denver): arXiv export API abstract; arXiv HTML v1 opened (repo + evidence-v1.1 links); GitHub API: repo BiVelio/caleta, Apache-2.0, created 2026-10-28, last push 2026-11-04, tags evidence-v1.0 / evidence-v1.1, no releases; README read (v0.1.0 experimental). Not run.

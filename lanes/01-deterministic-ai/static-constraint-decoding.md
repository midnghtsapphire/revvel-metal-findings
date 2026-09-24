# STATIC (static-constraint-decoding)

```json
{
  "id": "static-constraint-decoding",
  "name": "STATIC",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/youtube/static-constraint-decoding",
    "https://arxiv.org/abs/2602.22647"
  ],
  "license": "Apache-2.0",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Closed-set deliver:* allowlist / Semantic-ID masks — accelerator-native sparse-trie index; not a CFG replacement for wr:code grammars",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-24"
}
```

Official **STATIC** (Sparse Transition-Accelerated Trie Index for Constrained decoding) from YouTube / Google Research. Enforces outputs stay inside a **prespecified finite set of token sequences** during autoregressive decode. Offline `build_static_index` builds a hybrid dense-prefix + CSR-sparse-tail index; online `sparse_transition_{jax,torch}` applies a vectorized accelerator-native mask (O(1) I/O vs total constraint count; O(log K) vs branching). JAX/TPU + PyTorch/GPU kernels, benchmarks vs Naive Trie / Hashmap / PPV, unit tests. Paper: arXiv 2602.22647 (*Vectorizing the Trie…*, Su et al., 2026). Apache-2.0; 237★.

**Revvel hit:** when `deliver:*` needs a **closed allowlist** (enum of Semantic IDs, fixed label strings, sealed ticket IDs) rather than a full CFG, STATIC is the metal mask path — preprocess the allowlist once, keep the same WR contract. For open WR/code grammars stay on **xgrammar-2** / **llguidance** / **cfgzip** / **vocab-mask-trie**. Do **not** treat as a PSC/CFG drop-in.

**Honesty:** CAN-PARTIAL. Verified 2026-09-24 (America/Denver): GitHub `youtube/static-constraint-decoding` live (237★, Apache-2.0 LICENSE, Python); tree `static_decoding/{csr_utils,decoding_jax,decoding_pt}.py` + `benchmarks/` + `tests/` + `example.ipynb`; arXiv 2602.22647 live. **Repo is archived** (read-only; last push 2026-09-01). Finite allowlist / Semantic-ID sequences — **not** full CFG. No vLLM/SGLang serving plugin (research JAX/PyTorch kernels only). Still metal for closed-set `deliver:*` masks.

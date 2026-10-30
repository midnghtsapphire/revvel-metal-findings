# dispinv

```json
{
  "id": "dispinv",
  "name": "dispinv (dispatch-pinned batch invariance for vLLM on Hopper)",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/C-C-Hao/dispinv",
    "https://github.com/C-C-Hao/dispinv/blob/main/docs/design.md"
  ],
  "license": "Apache-2.0",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Borrow the qualification pattern only: a self-hosted replay engine must prove its determinism switch is live (fail closed with a non-zero exit when it is not) and pass a fault-injection negative control before its outputs count as evidence. Not for adoption: brand new, monkeypatches vLLM, H200/SM90 only.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-30"
}
```

**dispinv** (`C-C-Hao/dispinv`, Apache-2.0; repo created 2026-10-30 05:50 MDT, one commit `ff39fe731e` "Initial public release of dispinv 0.1.1"; not on PyPI). Batch-invariant vLLM inference on Hopper by **pinning kernel dispatch** instead of rewriting kernels: three modes (Strict / Split / KV-Reserve) pin the cuBLAS no-split-K path, the FlashAttention-3 split count and Inductor autotune choices so a request's logits do not depend on what else is in the batch. It loads through `sitecustomize` (monkeypatching), **fails closed** (exit code 70) when a pin cannot be applied, prints `PROOF` lines to stderr from each patched process (a server counts as in a mode only if its logs contain the listed lines), and ships a GPU validation script with a fault-injection negative control (`DISPINV_FAULT_INJECTION=batchstride`) that must make the check fail.

Requirements as stated: vLLM `main` at commit `36768d1bfd39094681cdbc8cb37d4b31c0729c89` (committed 2026-09-28 23:02 MDT; version string `0.30.1rc1.dev312+g36768d1bf`) plus a bundled patch `patches/vllm-36768d1-sm90-bypass.patch`, PyTorch 2.13.0+cu130, Triton 3.7.1, NVIDIA Hopper SM90 (cost-model constants for H200 SXM; not tested elsewhere). It does not track a vLLM release, so it lags the shipped `VLLM_BATCH_INVARIANT` path in vLLM 0.32.0. The accompanying paper is anonymous and under review (per `CITATION.cff`); no arXiv id yet.

**Revvel hit:** revvel-standards does not self-host a model, so nothing to install. The borrowable part is the qualification discipline for any future replay engine (see **vllm-batch-invariance**, **bitexact-llm**, **vosti**): (1) the engine refuses to start if its determinism mode is not actually in effect, (2) it logs which guarantees are live, and (3) the check is shown to fail under an injected fault, so a green check means something. Same shape as **bi-acceptance-gates**.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-30 (America/Denver): repo page and API (Apache-2.0, created date, single commit), README, docs/design.md, CITATION.cff, CHANGELOG and the boot hook read through the API (`_os._exit(70)` in `dispinv/boot/sitecustomize.py`), vLLM commit `36768d1b` resolves via the commits API, PyPI `dispinv` 404. Hours old, single commit, hardware-specific, monkeypatches upstream internals; results are the author's own and were not run here (no GPU).

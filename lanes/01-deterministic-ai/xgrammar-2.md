# XGrammar-2

```json
{
  "id": "xgrammar-2",
  "name": "XGrammar-2",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/mlc-ai/xgrammar/",
    "https://blog.mlc.ai/2026/05/04/xgrammar-2-fast-customizable-structured-generation",
    "https://arxiv.org/html/2601.04426v2",
    "https://doi.org/10.1145/3786335.3813124",
    "https://github.com/mlc-ai/xgrammar/security/advisories/GHSA-ggf7-2pq3-j6pv",
    "https://github.com/mlc-ai/xgrammar/security/advisories/GHSA-m5hf-r6jr-m4q6",
    "https://github.com/mlc-ai/xgrammar/security/advisories/GHSA-3gmq-qh92-5grm"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": ".github/workflows/openrouter-coder.yml + schemas/ — grammar-mask coder output — pin xgrammar >= 0.2.6 (2026-10-04 advisories: grammar/regex compile DoS + memory-safety from untrusted input)",
  "honesty": "CAN",
  "acquired": "2026-08-22",
  "updated": "2026-10-19"
}
```

Constrained decoding engine. Compiles a CFG / JSON Schema / structural tag into a token mask. Invalid tokens get probability 0. XGrammar-2 (May 2026) adds TagDispatch and cross-grammar cache for agentic, mid-request structure changes. Default structured-gen backend in vLLM, SGLang, TensorRT-LLM, MLC-LLM. Paper: ACM Conference on AI and Agentic Systems 2026.

This is the closest thing to machine language on the *generation* side: the automaton sits on the logits.

**Revvel hit:** `openrouter-coder.yml` currently hopes the model emits a usable patch. Bind it to `schemas/` (WR packet, state, deliver matrix). Malformed coder output should be physically impossible. That is how you stop WR essays and start `wr:code`.

**Caveat:** temperature=0 + grammar ≠ bit-identical across GPUs/kernels. Structure is deterministic. Token choice among legal tokens is not always.

**Next trial:** take `schemas/state.schema.json` from revvel-standards, compile it with XGrammar or an OpenRouter/vLLM structured-output path, generate 50 packets, assert 50/50 parse.

**Update 2026-10-13 (security floor):** three XGrammar advisories were published 2026-10-04 (MDT), all patched in **0.2.6**: **GHSA-ggf7-2pq3-j6pv** (high, null-byte memory-safety violation in `RegexConverter`, affects <= 0.1.33), **GHSA-m5hf-r6jr-m4q6** (high, two denial-of-service crashes in `compile_regex` / `compile_grammar` from untrusted input, < 0.2.6), **GHSA-3gmq-qh92-5grm** (medium, out-of-bounds write via deserialized nullable rule IDs, >= 0.1.23 < 0.2.6). No CVE IDs assigned yet. This matters for wr:code because the grammar/schema is compiled from repo content (`schemas/`, WR packets). If any of that text can come from an issue or PR, it is untrusted input to the compiler. **Pin `xgrammar >= 0.2.6`** on any self-hosted path; latest is **0.2.8** (PyPI, 2026-09-24). Engines already above the floor: vLLM **v0.31.0** pins `xgrammar == 0.2.7` (`requirements/common.txt`), SGLang **v0.5.21** pins `xgrammar==0.2.7`. Older engine images that bundle < 0.2.6 need a bump. Separately, vLLM published five advisories on 2026-10-09 (stop_token_ids OOB/DoS fixed in 0.29.0; video frame-cap bypass fixed in 0.31.0; the other three fixed in 0.24.0–0.30.0), so the self-hosted serving floor is **vLLM >= 0.31.0**. License confirmed Apache-2.0 via the GitHub API. Verified 2026-10-13 (America/Denver) via the GitHub security-advisories API + advisory pages (200), PyPI JSON, and engine requirement files at the release tags.

**Update 2026-10-19:** no new XGrammar release (PyPI and GitHub latest still **0.2.8**, 2026-09-24). Engine pins moved up: vLLM **v0.32.0** (2026-10-18) `requirements/common.txt` pins `xgrammar == 0.2.8` (and `llguidance >= 1.7.0, < 1.8.0`, `outlines_core == 0.2.14`), and its release notes add xgrammar `propertyNames` support (#57594). Both are above the >= 0.2.6 floor. SGLang **v0.5.22** (GitHub release 2026-10-18 20:55 MDT) notes an important fix where hybrid linear models could resume from wrong mamba states when speculative decoding and structured output were used together (#43029); pin requirement not rechecked. Verified 2026-10-19 (America/Denver) via PyPI JSON, GitHub releases API, raw requirements at the vLLM tag.

# agrepl

```json
{
  "id": "agrepl",
  "name": "agrepl",
  "lane": "02-formal-replay",
  "status": "watching",
  "urls": [
    "https://github.com/Taiwrash/agrepl",
    "https://arxiv.org/abs/2607.16200"
  ],
  "license": "MIT (README; no LICENSE file at root)",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "wr:code repro — record a coder run's LLM/API traffic through a local MITM proxy with no SDK or code change, then replay it in isolation with zero outbound network; noise-aware diff separates real agent drift from CDN/timestamp header noise",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-07"
}
```

**agrepl** -- Go 1.22 single static binary for deterministic replay of agent runs. `record` forks the child process with `HTTP_PROXY`/`HTTPS_PROXY` pointed at a local goproxy-based MITM (local root CA injected), serialises every exchange as a JSON trace, and `replay` serves them back by canonical request-key lookup with zero network calls, so it works with Python, Node, Go, curl, or any CLI. Strict replay by default, `--fallback` for unmatched requests; structural JSON matching and binary payloads supported. Paper: "Deterministic Replay for AI Agent Systems" (arXiv 2607.16200, submitted 2026-04-30) formalises the request-key function, proves the determinism invariant, and reports replay fidelity F = 1.0 over 250 replays. Repo tip `4ab694e1c4913e6dd183373971206f06d392d717` (2026-09-07); ~30★; no tags.

**Revvel hit:** language-agnostic replay for the Node coder path when a `wr:code` run misbehaves: record once, replay the exact run offline while fixing the labeler or prompt. Complements **chronicle** (cut-point regression tests) and overlaps **agentape** (process-boundary cassettes).

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-07 (America/Denver): repo and arXiv abstract live. MIT is stated in the README badge and paper, but there is no LICENSE file at the root; get that fixed before vendoring. CI/CD regression mode, SDK wrappers, and gRPC/HTTP2 matching are still unchecked roadmap items; remote push/pull uses Cloudflare R2. Keep **agentape** / **chronicle** as primary until CI mode ships.

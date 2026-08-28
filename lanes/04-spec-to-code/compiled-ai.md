# Compiled AI

```json
{
  "id": "compiled-ai",
  "name": "Compiled AI (Code Factory)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2604.05150",
    "https://github.com/XY-Corp/Compiled-AI"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "research:complete → wr:code / spec-approved: compile WR once, then deterministic deliver:* (LLM out of the control plane)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-28"
}
```

LLM generates a bounded artifact **once** from a YAML spec. Four-stage gate (security → syntax → execution → accuracy) then the control plane runs as static code. Runtime LLM, if any, is a bounded tool call with schema fixed at compile time. Paper (XY.AI / Stanford / Cornell / Harvard, 2026): BFCL n=400, 96% compile success then 100% deployed reliability, N* ≈ 17 vs Direct LLM, 57× tokens at 1k tx. Repo MIT, README + LICENSE live 2026-08-28.

**Revvel hit:** this is the wr:code architecture, not another agent. Map YAML-spec → four-stage validation onto the existing `openrouter-coder.yml` + `schemas/` contract. Do not stand up Temporal as a second spine (that finding stays watching). The stall after `research:complete` is an uncompiled essay; Compiled AI is compile-then-ship.

**Honesty:** CAN-PARTIAL. Paper + GitHub verified. Not a drop-in for `orchestrate.js`. Pattern only.

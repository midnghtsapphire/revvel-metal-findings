# agency-harness

```json
{
  "id": "agency-harness",
  "name": "Agency: System Optimizations for Cost-Efficient Agent Harnesses",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.12122",
    "https://arxiv.org/html/2611.12122v1"
  ],
  "license": "n/a (paper; no Agency code URL found; HTML cites headroomlabs-ai/headroom and rtk-ai/rtk as related tools)",
  "metal": 2,
  "determinism": 3,
  "revvel_hit": "Harness-side, model-unchanged cost cuts: an interposition layer between Claude Code / Codex and the model reduced cost up to 35% on real benchmarks without accuracy loss (authors). Prior work they cite: harness variance moves cost up to 2.6x but barely moves accuracy. For revvel-standards this argues for measuring wr:code token/call counts per run and trimming repeated context in the existing coder harness, not swapping models.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-11"
}
```

**Agency** (arXiv **2611.12122** v1, submitted 2026-11-09). Analyzes where tokens and LLM calls pile up across agent traces and builds a harness interposition platform with one abstraction for portable optimizations on off-the-shelf harnesses. Proof-of-concept optimizations cut cost up to 35% across real-world benchmarks without hurting accuracy (authors).

**Revvel hit:** pairs with FlowPlan: both say the cheapest speedup for the wr:code coder is in the harness, not the model. First step is a per-run token and call count in the existing run record, so any trial has a baseline. No new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-11 (America/Denver): arXiv export API abstract; HTML v1 opened; no Agency repository link (only related tools headroom and rtk). Not run. Numbers are the authors'.

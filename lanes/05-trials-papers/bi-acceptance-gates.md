# bi-acceptance-gates

```json
{
  "id": "bi-acceptance-gates",
  "name": "God Does Not Play Dice: batch-invariance acceptance gates for agent-generated kernels",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.36623",
    "https://arxiv.org/html/2610.36623v1"
  ],
  "license": "arXiv paper (no code release found)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Pattern for any wr:code output that is performance code: put determinism checks as successive acceptance gates (static contract check, then dynamic bitwise compare across batch contexts) before benchmarking, and feed rejections back to the coder instead of merging a faster-but-nondeterministic candidate",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-28"
}
```

**God Does Not Play Dice: Enforcing Batch Invariance in Agentic Kernel Generation** (Youwei Bao, Chengpeng Wang, Simin Chen). arXiv **2610.36623**, submitted 2026-10-26 22:27 MDT (cs.AI / cs.LG / cs.SE).

Kernel-writing agents optimize for correctness and speed but ignore batch invariance (BI): the same request can give different bits depending on what else is in the batch. The authors report **19 confirmed BI violations among 83 batch-applicable released artifacts**. Their tool (unnamed in the abstract) combines contract-guided static dependency analysis with dynamic validation of bitwise consistency across batch contexts, plugged into the agent's optimization loop as **successive acceptance gates**: structurally risky or dynamically non-invariant candidates are rejected before performance benchmarking, with feedback returned to the agent. Across three agent frameworks it raises the BI pass rate from **67.6% to 91.9%** while keeping **91.8%** of the baseline geometric-mean speedup (authors' numbers).

**Revvel hit:** the gate ordering is the borrowable part: cheap static check, then a bitwise replay across contexts, then and only then the speed benchmark, all inside the existing wr:code check rather than a new pipeline. Directly relevant if revvel-standards ever self-hosts inference or accepts GPU/kernel code from the coder; pairs with **vllm-batch-invariance**, **bitexact-llm** and **deepinfer** (01) for the runtime side.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-28 (America/Denver): arXiv abs 200, API metadata and abstract read, HTML v1 scanned for links (only references to thinking-machines-lab/batch_invariant_ops and flashinfer-ai/mlsys26-agent-baseline; no code link for the tool itself). Not peer-reviewed; results are the authors' own; nothing run.

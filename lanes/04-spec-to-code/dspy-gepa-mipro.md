# DSPy — GEPA + MIPROv2

```json
{
  "id": "dspy-gepa-mipro",
  "name": "DSPy GEPA / MIPROv2 compile",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://dspy.ai/diving-deeper/choosing-an-optimizer/",
    "https://dspy.ai/api/optimizers/MIPROv2/",
    "https://github.com/stanfordnlp/dspy/blob/main/docs/docs/diving-deeper/gepa-in-depth.md",
    "https://arxiv.org/abs/2406.11695",
    "https://arxiv.org/abs/2507.19457"
  ],
  "license": "confirm on repo",
  "metal": 2,
  "determinism": 3,
  "revvel_hit": "Compile the research-complete → wr:code classifier; do not hand-tune openrouter-assignee prompts",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

DSPy treats the pipeline as a program. `.compile(program, trainset)` searches instructions and demos against a metric.

- **MIPROv2**: Bayesian search over the joint instruction + few-shot space. `auto` = light/medium/heavy. Paper: arXiv 2406.11695.
- **GEPA**: reflective evolutionary search. Metric returns `score` + natural-language `feedback`. Pareto frontier of programs. Paper: arXiv 2507.19457. Docs name `seed=0` on the constructor.

This is **not** near-metal. It is the discipline for the missing label. The stall in START_HERE is a program with no metric: research finishes, nobody applies `wr:code`.

**Revvel hit:** define a tiny module: input = research packet + honesty table, output = one label. Metric = did a human (or later, CI) agree, and did a coder PR actually open. Compile it. Pair the output signature with XGrammar/GBNF so the label is one of three tokens, not a paragraph.

**Caveat:** compile is stochastic across runs unless you pin seeds and freeze the teacher. Determinism here is *the metric and the output schema*, not bit-identical prompts.

**Next trial:** 30 historical `[WR]` issues from revvel-standards (research-complete vs never-coded). Train/val split. Compile GEPA with `seed=0`. Report precision on `wr:code`. If it cannot beat “always wait for a human”, mark dropped.

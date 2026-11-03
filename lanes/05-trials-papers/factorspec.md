# factorspec

```json
{
  "id": "factorspec",
  "name": "FactorSpec: exact relational constraints served as speculative drafts",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.02297"
  ],
  "license": "UNKNOWN (no code released)",
  "metal": 3,
  "determinism": 4,
  "revvel_hit": "Self-hosted coder only: goes past grammar masks (syntax) to exact cross-field relations compiled from a JSON Schema into a factor graph, and turns every forced token into a free speculative draft (up to 1.43x faster decode, up to 13.9x valid records per GPU-second vs syntax-only, SGLang + vLLM). Relevant if WR packets / deliver:* records with cross-field rules are ever decoded on our own GPUs. No code; watch.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-03"
}
```

**FactorSpec: Serving Exact Relational Constraints as Speculative Drafts** (Jianchang Su, Dawei Xiang, Wei Zhang). arXiv **2611.02297** v1, submitted 2026-11-01 16:46 MST (cs.LG). No code link in the abstract or HTML version.

Method (abstract): compile a JSON Schema **plus relations among its fields** into a factor graph with an exact feasibility check; draft every token the constraint determines as certain; verify each request at a per-request width; compute masks in worker processes outside the scheduler while the GPU runs.

Authors' numbers: on NATURAL PLAN trip problems Qwen3-8B writes a valid itinerary 10% of the time (14% with retries naming the violated relation); in SGLang FactorSpec drafts up to 10.5 tokens per verify step (up to 1.9x the fastest n-gram drafter), decodes up to 1.43x faster than per-load-tuned speculators at a grammar mask's cost, also leads in vLLM, and serves up to 13.9x the valid records per GPU-second of syntax-only baselines.

**Revvel hit:** lane-01 engines (xgrammar-2, llguidance, glrmask) only guarantee shape; cd-scale-semantic-gap already warns schema != semantics. FactorSpec is the first serving-side answer for exact cross-field rules. Only matters for a self-hosted coder; standing hunt for code.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-03 (America/Denver): arXiv export API metadata + abstract, abs page 200, HTML version checked for code links (none). Results are the authors'.

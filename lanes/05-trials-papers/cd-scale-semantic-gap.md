# CD × scale semantic gap (small-LLM structured benchmark)

```json
{
  "id": "cd-scale-semantic-gap",
  "name": "CD × scale semantic gap",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2609.23742",
    "https://arxiv.org/pdf/2609.23742",
    "https://github.com/CruiseDevice/small-llm-structured-benchmark"
  ],
  "license": "unknown",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "Honesty gate for wr:code / deliver:* — CD (Outlines/XGrammar) guarantees schema validity not semantic correctness; keep contract-agent + agentverify + agent-spec for content",
  "honesty": "CAN",
  "acquired": "2026-09-28"
}
```

**Constrained Decoding Eliminates Structural Failures in Small LLMs but Reveals a Scale-Dependent Semantic Gap** (Chavan, arXiv 2609.23742, submitted ~2026-09-20). Controlled size-ladder (0.6B–4B; Qwen3 / Llama 3.2 / Phi-4-mini) × 14 structured tasks × native / Outlines / XGrammar. Two-axis metric: structural (schema validity) vs semantic (content accuracy). Result: CD lifts schema validity to **100%** everywhere, but content accuracy stays scale-dependent — type coercion is CD-rescuable; instruction-semantic failures (e.g. multi-step tool calls) are **CD-resistant**. XGrammar near-zero overhead vs Outlines compile tax. Code + task suite: `CruiseDevice/small-llm-structured-benchmark` (tag `v1.0` frozen to paper); notebook-driven; `pip install outlines xgrammar` for phase 3.

**Revvel hit:** do not treat **xgrammar-2** / **llguidance** / **outlines** / **gramr** masks as sufficient for `deliver:*` correctness. Masks kill malformed WR JSON; they do not prove the right tools fired or the right fields filled. Keep **contract-agent** (CEL refuse), **agentverify** (cassette CI), and **agent-spec** (lifecycle) as the semantic/behavioral layer. Prefer XGrammar-class engines for the structural cage when self-hosting small coder models.

**Honesty:** CAN for the empirical claim (paper abs+pdf 200; GitHub code drop live 2026-09-28 America/Denver). License file not present at repo root this pass (unknown). Benchmark / study — not a serving plugin. Citation bibtex in README still has placeholder arXiv id; use **2609.23742**.

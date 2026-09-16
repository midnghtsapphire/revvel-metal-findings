# SWYB — Stay Within Your Bounds (Distance-Guided CFG Decode)

```json
{
  "id": "swyb",
  "name": "SWYB (Stay Within Your Bounds)",
  "lane": "05-trials-papers",
  "status": "active",
  "urls": [
    "https://arxiv.org/abs/2608.28229",
    "https://github.com/Enzossssss/SWYB"
  ],
  "license": "CC-BY-SA-4.0",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "General CFG acceptance under finite token budget (JSON/SQL beyond LL(1) TruncProof)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-16"
}
```

Findings of EMNLP 2026. PDA-based distance-to-acceptance decoding for **general CFGs**: offline bounded pushdown summaries + online horizon-aware pruning / beam search. Guarantees every finished string is accepted by the target grammar (not just locally prefix-feasible).

Eval on Text-to-JSON, Text-to-SQL, Text-to-LTL. Code + tutorial notebook live at `Enzossssss/SWYB`.

**Revvel hit:** generalizes TruncProof’s budget idea past LL(1) JSON — useful if `wr:code` / schema dumps need SQL-ish or richer CFG cages under a hard token ceiling. Research decoder only; keep vendor/XGrammar as the production mask.

**Honesty:** paper URL + GitHub verified live this scrape. CC-BY-SA share-alike on derivatives.

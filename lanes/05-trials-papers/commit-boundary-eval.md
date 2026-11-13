# commit-boundary-eval

```json
{
  "id": "commit-boundary-eval",
  "name": "Commit-boundary evaluator: rule-based write-expected vs write-committed check beats LLM judges on tau2-bench",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.14581",
    "https://arxiv.org/html/2611.14581",
    "https://doi.org/10.5281/zenodo.23683806",
    "https://zenodo.org/records/23683806"
  ],
  "license": "replication package: code MIT, data and docs CC BY 4.0 (per Zenodo record); paper arXiv",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "Deterministic deliver:* gate pattern. For each work item, record one gold bit (does this item expect a write: a commit/PR/merge?) and compare it with what the trace shows actually committed. Four labels: correct_action, missed_action, premature_commitment, correct_refusal. No model call; same input, same output. On 2,160 tau2-bench episodes the LLM judge passed 10-11 of 11 forbidden writes (a stronger judge still passed 6); the boundary check caught all 11. Applied to revvel-standards: a deliver:* or merge that happens on an item not marked spec-approved/assigned is premature_commitment; a spec-approved item that closes with no commit is missed_action. Matches Audrey's rule that nothing merges unless its work item was assigned and finished.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-13"
}
```

**When Evaluators of AI Agents Disagree** (arXiv **2611.14581**, Sungbin Im, submitted 2026-11-10, cs.SE/cs.AI/cs.CR; submitted to Empirical Software Engineering). Scores 2,160 tau2-bench airline/retail episodes four ways: native gold-state scoring, an LLM judge, a policy-aware judge, and a minimal rule-based boundary evaluator. The judge was self-consistent (98.2%) but agreed with native scoring only 56.2% of the time. Forbidden writes occurred in 11.1% of ungated episodes; verification, correction and safe-termination gates did not reduce them significantly, and the traces point to the gates' evidence digest dropping order status and customer auth. Limitation (authors): correct_action only means an expected write happened, not that its content was right.

**Revvel hit:** add the boundary labels as a cheap pre-check in the existing deliver:* gate (no new pipeline). It needs only a per-item 'expects write' flag, which the spec-approved label already implies. Second lesson: if a gate summarizes evidence before deciding, check the summary keeps the fields the rule needs.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-13 (America/Denver): arXiv abs page opened; Zenodo API record 23683806 opened (open access, v9, artifact_v9.zip 6.8 MB, code MIT / data CC BY 4.0, benchmark sierra-research/tau2-bench @ 363133a). Artifact zip not downloaded; numbers are the author's.

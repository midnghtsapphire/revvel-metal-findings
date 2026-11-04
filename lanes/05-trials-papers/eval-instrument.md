# eval-instrument

```json
{
  "id": "eval-instrument",
  "name": "Silent Instrument Errors Reorder Agent Leaderboards",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.04399",
    "https://github.com/YangzeLiu/eval-instrument-disclosure"
  ],
  "license": "none declared (repo API: no license) - borrow checks only",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Any eval harness revvel-standards uses to score coder runs (BOBA-style chains, attested receipts, agent-evidence-vectors corpora) is part of the measurement and can fail silently. Cheap checks to copy: report the graded fraction (ungraded episodes must not count as failures or passes), aggregate cost from root spans only, tag the provenance of every recorded action (agent vs grader), pin evaluator versions and publish a re-grade diff on upgrade. Same rule as attested 0.1.1 'zero tests passed = FAILED'.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-04"
}
```

**Silent Instrument Errors Reorder Agent Leaderboards** (Yangze Liu). arXiv **2611.04399** v1, submitted 2026-11-03. Reproduction material: `YangzeLiu/eval-instrument-disclosure` (no license declared per repo API; maintainer reports for HAL and tau2-bench, corrections, a reproduction zip).

Authors' findings from published artifacts of HAL and tau2-bench: a general agent's 13-point gap on an airline benchmark came from about half its episodes never being graded and stored as failures; a cost column double-counted nested model calls; archived trajectories recorded grader-written actions as agent actions; a mode check misreading four files dropped scores by 59 to 82 points with no error. HAL maintainers confirmed three within five weeks.

**Revvel hit:** checks for the fleet's own eval/required-check scripts: graded fraction reported, root-span cost, action provenance tags, pinned evaluator + re-grade diff. Pairs with attested (zero passed tests = FAILED) and the agent-evidence-vectors pin discipline. No license on the repo, so borrow the checks as ideas only; do not copy code.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-04 (America/Denver): arXiv export API metadata + full abstract (code link in comment); repo API (no license, dates) and root listing. Not run. Results are the author's.

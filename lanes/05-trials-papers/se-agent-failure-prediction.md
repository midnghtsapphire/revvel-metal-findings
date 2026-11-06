# se-agent-failure-prediction

```json
{
  "id": "se-agent-failure-prediction",
  "name": "Hard Issue, Weak Model, or Bad Run? Rethinking Failure Prediction for Coding Agents",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.08285",
    "https://arxiv.org/html/2611.08285"
  ],
  "license": "n/a (paper; no dedicated code artifact; uses public SWE-bench Verified trajectories)",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Trajectory-based mid-run failure predictors mostly predict issue difficulty and model ability, not the run. Issue difficulty alone reaches 0.92 AUROC vs ~0.62 for trajectory predictors (authors). For wr:code stop/retry: do not gate retries on a mid-run trajectory classifier; prefer issue difficulty + model ability priors, and spend budget on retries that can rescue bad runs rather than hard issues.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-06"
}
```

**Hard Issue, Weak Model, or Bad Run?** (Shi & Assunção). arXiv **2611.08285** v1, submitted 2026-11-05. On public SWE-bench Verified trajectories (one attempt per model per issue), two run-independent factors dominate failure prediction: a difficulty score that never looks at the run reaches **0.92 AUROC**, while trajectory predictors reach about **0.62**. Within an issue, knowing which model ran predicts failure better than the predictors; beyond difficulty and ability, trajectory gain is statistically equivalent to zero (authors). Model switching gains nothing on held-out runs beyond random variation; retries can rescue bad runs but not issues beyond the model's ability, and current predictors cannot tell those causes apart.

**Revvel hit:** evidence against wiring a mid-run trajectory "going wrong" classifier into wr:code stop/retry. Prefer static priors (issue difficulty, model ability) and equal-budget retry policy; leave mid-run predictors out of the spine.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-06 (America/Denver): arXiv export API abstract; arXiv HTML opened (links only to mini-swe-agent as cited tool, no paper artifact repo). Not run. Numbers are the authors'.

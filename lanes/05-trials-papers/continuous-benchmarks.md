# continuous-benchmarks

```json
{
  "id": "continuous-benchmarks",
  "name": "Benchmarks as Software: Terminal-Bench and Continuous Benchmarks",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.08417",
    "https://arxiv.org/html/2611.08417",
    "https://github.com/harbor-framework/terminal-bench-2-1",
    "https://github.com/harbor-framework/terminal-bench-2"
  ],
  "license": "n/a for paper; Terminal-Bench repair release linked as harbor-framework/terminal-bench-2-1 (verify license before any borrow of code)",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Continuous-validation workflow for agentic benchmarks: community reports + task artifacts + agent traces + automated oracle checks + human-gated repairs. Applied to Terminal-Bench 2.0; ~30% of tasks had issues; repairs shipped as 2.1 and moved accuracy >10pp / ranks up to 3 (authors). Resource budgets (wall-clock) are part of the measurement spec. Borrow the maintenance loop for fleet evals beside eval-instrument; do not adopt Terminal-Bench as a second pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-06"
}
```

**Benchmarks as Software: Terminal-Bench and the Case for Continuous Benchmarks** (Buchanan, Zhou, Linderman, Ré). arXiv **2611.08417** v1, submitted 2026-11-05. Even carefully validated agentic benchmarks accumulate **benchmark maintenance debt** as models find valid solutions verifiers reject and infra changes break task assumptions. The paper's continuous-validation workflow combines community reports, task artifacts, agent traces, automated oracle checks, and human-gated repairs. Audit of Terminal-Bench 2.0 found issues in roughly **30%** of the benchmark; repairs released as Terminal-Bench 2.1 changed accuracy by over **10 percentage points** and moved leaderboard positions by up to **three ranks** (Spearman ρ = 0.958). Fixed wall-clock budgets also change conclusions (example: extending the time limit closes a 20pp harness gap on GPT 5.4; authors).

**Revvel hit:** same family as **eval-instrument**: keep fleet eval scores honest by continuous oracle + human-gated repair, and treat resource budgets as part of the pinned measurement. Pattern only; no new eval pipeline in revvel-standards.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-06 (America/Denver): arXiv export API abstract; arXiv HTML (links `harbor-framework/terminal-bench-2`, `terminal-bench-2-1`, TASK_REVIEW_AUTOMATION.md); GitHub pages for terminal-bench-2 and terminal-bench-2-1 returned 200. Code not run; license of the repair repos not adopted.

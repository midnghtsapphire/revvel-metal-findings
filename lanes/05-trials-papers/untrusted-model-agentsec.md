# untrusted-model-agentsec

```json
{
  "id": "untrusted-model-agentsec",
  "name": "Treating the Model as an Untrusted Component: deterministic policy enforcement, human approval and taint tracking",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.11571",
    "https://github.com/nawaralseelawi/untrusted-model-agentsec"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Evidence for the deliver:* gate design: a task-bound deterministic monitor outside the model held severe actions at 0.0% in simulation where every prompt-guardrail stack reached 100% under an adaptive attacker; a human approval layer without a deterministic monitor fails to approval spamming unless each episode has a deterministic approval budget; monitor implementation quality matters (naive 18/33 attack variants admitted, hardened 6, capability-bound 1). Borrow: capability-bound allowlist per WR + per-run approval budget in the existing mcp-hangar / verax gate.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-10"
}
```

**Treating the Model as an Untrusted Component** (Aljumaily, Alseelawi, Alshabandar). arXiv **2611.11571** v1, submitted 2026-11-08. Compares in-prompt defences (hardened prompts, spotlighting, LLM detectors) with four deterministic reference monitors, human approval and taint tracking, judged by one effect-based oracle in an executable environment (13 tasks, 12 tools, argument-fuzzing attackers, severity-weighted harm). Real-model runs on Qwen2.5-1.5B/7B (156 attack episodes per defence and model): the models proposed the attacker's call in 64% / 84% of episodes behind the task-bound monitor, which admitted 1.3% / 7.7%. Human-approval and taint results are simulation-only; the authors flag that the larger model's detector result contradicts their assumed erosion law.

**Revvel hit:** supports what the 04-spec-to-code gates already do (deny-by-default, outside the model) and adds one concrete knob: a deterministic approval budget per deliver:* run, so a human approver can't be spammed into clicking through. Goes in the existing gate config; no new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-10 (America/Denver): arXiv export API abstract + comment (code URL); HTML v1 opened; GitHub API: repo MIT, created 2026-11-05, pushed 2026-11-08, contents listed (run_all.sh, results.json, pilot_real_v1/v2, notebooks). Not run. Numbers are the authors'.

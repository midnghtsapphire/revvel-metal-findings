# agenttrustci

```json
{
  "id": "agenttrustci",
  "name": "AgentTrustCI: policy, grounding and trajectory tests for LLM agents in CI",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.06674",
    "https://github.com/sachinkg12/agenttrustci"
  ],
  "license": "none declared (repo API license null); borrow the idea only",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Build-time checks over recorded agent traces, replayed deterministically: policy (forbidden tools/args), grounding (claims backed by tool output) and trajectory (step order and count). For revvel-standards: record the deliver:* coder's tool-call trace and assert policy/trajectory rules on it as a job on revvel-engine-spine.yml, with no model in the check. Java/JUnit 5 and unlicensed, so do not depend on it.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-05"
}
```

**AgentTrustCI** (Sachin Gupta, ICCA 2026). arXiv **2611.06674**. A Java / JUnit 5 framework that runs agent-behavior checks inside the normal test run: policy, grounding and trajectory assertions over recorded traces, replayed deterministically so CI does not call a model. Authors' result: all 55 synthetic cases classified correctly (synthetic only, self-run). Repo `sachinkg12/agenttrustci`: "(Experimental)", Maven `pom.xml`, `src/`, `experiments/`; no license; last push 2026-06-13; no releases or tags.

**Revvel hit:** the trace-replay assertion style fits the wr:code to deliver:* check: a deterministic test that the coder used only allowed tools, in an allowed order, and that its PR claims match tool output. Implement as revvel's own check under insertion point 5 (a job on the spine); borrow the three check families only.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-05 (America/Denver): arXiv export API abstract; arXiv HTML (links the repo); repo API (license null, pushed 2026-06-13), root listing, releases and tags (none). Code not run.

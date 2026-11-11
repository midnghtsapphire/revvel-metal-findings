# flowplan

```json
{
  "id": "flowplan",
  "name": "FlowPlan: Abstraction-Guided Planning and Verification for Coding Agents",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.13241",
    "https://arxiv.org/html/2611.13241v1",
    "https://github.com/MelikaSepidband/FlowPlan"
  ],
  "license": "none declared (GitHub API license null) - borrow the idea, do not vendor code",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "Speed on the wr:code coder loop: plan the repair as typed graph deltas on a per-function CFG/DFG before editing, then flow_check compares the rebuilt graph to the plan (exact / same_family / mismatch) and a final verify runs before stop. Authors report 0.32-0.76x baseline tokens (Haiku 4.5 / Sonnet 5 on SWE-bench Verified/Pro, SecBench) with no significant change in resolution rate. The plan-vs-observed delta is a machine-checkable completion bit for deliver:* that fits beside the existing settle gate (cadence), not a new pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-11"
}
```

**FlowPlan** (arXiv **2611.13241** v1, submitted 2026-11-09). Replication package at `MelikaSepidband/FlowPlan`: an MCP server with five tools (`flow_of`, `flow_locate`, `flow_plan`, `flow_check`, verify) plus a `/flowfix` skill attached to a vanilla Claude Code session, the harness for SWE-bench Pro / Verified / SecBench, and reproductions of five token-reduction baselines. Tokens drop because post-edit re-reading and re-testing is replaced by an explicit plan-vs-observed graph check and smaller per-call context.

**Revvel hit:** the wr:code coder could record its intended change as graph deltas in the spec-approved packet and the deliver:* check could compare them with the rebuilt graph. Insertion point 5 (a job on `revvel-engine-spine.yml`) or a coder-side MCP tool behind the existing gate. Do not open a second pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-11 (America/Denver): arXiv export API abstract; HTML v1 opened (links the repo); GitHub API (created 2026-08-17, pushed 2026-10-02, no license); README read. Not run. Numbers are the authors'.

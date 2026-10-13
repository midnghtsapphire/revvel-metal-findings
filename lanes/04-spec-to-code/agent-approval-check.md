# agent-approval-check

```json
{
  "id": "agent-approval-check",
  "name": "Agent Approval Check (anthropics/claude-code-action)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/anthropics/claude-code-action/tree/main/agent-approval-check",
    "https://github.com/anthropics/claude-code-action/blob/main/agent-approval-check/action.yml",
    "https://github.com/anthropics/claude-code-action/commit/846d5d8993b09aeea48c5cdde44b7c68f0ba24bc"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "deliver:* merge side: required `agent-approval-check` commit status on main; any PR with agent-authored commits needs N distinct human approvals from write-access users (native Approve or `/approve <head-sha>`); bot approvals never count, a new push makes old `/approve` stale, any error stays non-success. Set agent_logins / excluded_approvers from the TRUSTED_BOTS list in `trusted-bot-auto-approve.yml`",
  "honesty": "CAN",
  "acquired": "2026-10-13"
}
```

**Agent Approval Check** -- composite GitHub Action in `anthropics/claude-code-action` ("the same gate Anthropic runs internally on every agent-authored PR"). On PR open/push/comment it scans commits, PR author, and reviews for configured agent identities (`agent_emails`, `agent_logins`, or an optional base-branch `config_file`). If there are none, it posts `success: No agent activity`. Otherwise it counts **distinct human approvers**: the latest `APPROVED` review per login plus `/approve <sha>` comments whose SHA matches the **current head** (12–40 hex). Only users with write access count, checked per user through the collaborators permission API. Agent logins and `excluded_approvers` never count. The PR author's `/approve` counts as one. It posts the `agent-approval-check` commit status (`success` at `required_approvals`, default 2, otherwise `pending`) plus a sticky PR comment. Threat model in the README: runs only on `pull_request_target` + `issue_comment` (base-branch workflow, never checks out PR code); **fail-closed** (any unhandled error exits non-zero and the status stays non-success); PRs with >100 commits are treated as agent-authored; sibling-PR guard withholds `success` when another open PR to a protected base shares the head SHA; `exempt_head_branches` documented as unsafe. Runtime: `setup-python` pinned by SHA, `httpx==0.28.1`, `pyyaml==6.0.3`, `tenacity==9.1.4`, one script `agent_approval_check.py`.

Directory added in commit `846d5d8993b09aeea48c5cdde44b7c68f0ba24bc` (#1429, 2026-06-30 15:09 MDT); no later commits touch `agent-approval-check/` as of this scrape. Repo MIT (Copyright 2025 Anthropic, PBC), ~9.5k★, not archived, pushed 2026-10-09.

**Revvel hit:** revvel-standards already has the label side of the handoff (`spec-approval-gate.yml` → owner adds `spec-approved` → `openrouter-coder.yml`). The merge side still relies on branch protection plus bot auto-approve workflows (`trusted-bot-auto-approve.yml`, `auto-approve-clean-prs.yml`, both quiet-mode / `workflow_dispatch` only since 2026-07-25). Under plain branch protection, an approval submitted as `github-actions[bot]` counts. This check does not let it count. Feed the `TRUSTED_BOTS` logins (devin, jules, copilot, cursor, github-actions, …) into `agent_logins` and `excluded_approvers`, set `required_approvals: 1` for a single-owner repo, and mark `agent-approval-check` required on `main`. Pin `anthropics/claude-code-action/agent-approval-check@<reviewed SHA>`, not `@main`. It needs `pull_request_target` + `issue_comment` triggers. None of the existing hosts uses `pull_request_target`: `pr-governance-checks.yml` and `pr-state-orchestrator.yml` run on `pull_request`, and `revvel-engine-spine.yml` / `agent-fallback.yml` are `workflow_dispatch` only. So the check cannot sit inside one of them tamper-proof. That means **one small new workflow file** holding a single required status check. This is outside the five listed insertion points in `hits/revvel-standards.md`, so it needs an explicit owner OK. It is a gate, not a second pipeline: it never opens issues, dispatches, or labels, and it only posts a commit status and a PR comment.

**Honesty:** CAN. Verified 2026-10-13 (America/Denver): README, `action.yml`, script, and commit pages 200 on `main`; repo license MIT; directory history read from the GitHub API. The gate is deterministic (it counts approvals, and no model is involved). Caveats: it gates *merge*, not spec approval; protect `.github/workflows/` (CODEOWNERS / branch protection) or anyone who can push workflows can spoof the status; native Approve reviews are only picked up on the next push or `/approve` comment.

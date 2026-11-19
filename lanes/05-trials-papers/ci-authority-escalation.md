# ci-authority-escalation

```json
{
  "id": "ci-authority-escalation",
  "name": "Who Changed the AI Agent's Rules? Control-plane (workflow/permission) edits by coding agents carry 3.9x governance risk",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.23251"
  ],
  "license": "paper arXiv; AIDev dataset (third party)",
  "metal": 0,
  "determinism": 4,
  "revvel_hit": "Any wr:code / deliver:* PR that touches `.github/workflows/`, permissions, CODEOWNERS or branch-protection-style config is control-plane and should be held for Audrey (it already is by owner rule); this paper gives the deterministic path classifier and the numbers. 46.6% of agent control-plane PRs carry policy-violation flags, 63.6% of merged ones; all 775 extreme-risk PRs touched the control plane.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-19"
}
```

**Who Changed the AI Agent's Rules? Measuring How AI Coding Agents Escalate Authority in CI/CD Pipelines** (arXiv **2611.23251**, v1 submitted 2026-09-24, listed cs.SE 2026-11-19). Scores all 932,791 agent-authored PRs in AIDev (five agents) with a joint penalty P(M) of execution cost and governance risk; each PR is classified data-plane vs control-plane. Control-plane mean penalty 0.498 vs 0.218 (2.3x) and governance risk 0.530 vs 0.135 (3.9x). Mean joint penalty ranges 0.166 (Cursor) to 0.328 (Copilot), not explained by cost or merge rate. Manual check of 34 PRs (Cohen's kappa reported; value not read).

**Revvel hit:** a path rule in the existing deliver:* gate: a coder PR whose diff touches the control plane gets a `control-plane` label and cannot be silently merged, even when green (fits Audrey's 'escalate irreversible' rule and pairs with agent-approval-check / gh-actions-lock). No new workflow.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-19 (America/Denver): arXiv abs page opened. No code link on the abstract page; numbers are the authors'.

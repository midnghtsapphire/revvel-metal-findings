# caper

```json
{
  "id": "caper",
  "name": "Caper: consequence-aware approval for coding-agent shell commands",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.40753",
    "https://github.com/wudaoz/Caper",
    "https://github.com/wudaoz/Caper/tree/main/claude_code"
  ],
  "license": "Apache-2.0",
  "metal": 2,
  "determinism": 3,
  "revvel_hit": "Pattern for any deliver:* or wr:code command approval: approve what a command actually did, not what its text says. Run it once in a snapshotted, network-off container under strace, reduce the trace to a bounded effects report (file changes, network attempts, credential reads), let a separate approver decide, then commit the snapshot or roll it back. The trace and report are deterministic; the approver in the paper is an LLM, so only the report should gate on its own. Research code; borrow the pattern, no adoption.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-02"
}
```

**Caper: Consequence-Aware Approval for Coding-Agent Commands** (Wu, Chen, Sun, Shi, Lyu, David Lo). arXiv **2610.40753** v1, submitted 2026-10-29 10:20 MDT (cs.CR). Code: `wudaoz/Caper` (Apache-2.0 LICENSE; repo created 2026-10-20, last push 2026-10-20 05:19 MDT, 3 stars, 2 commits; Python 3.10+, Docker, Linux x86-64).

Four steps per shell command (README): (1) **pre-execute** -- snapshot the task container and run the command once inside it under `strace -f`, networking disabled, output held back; (2) **report** -- reduce the trace to a bounded effects report (persistent file changes, network attempts, user-visible output, the files each drew on, credential reads); (3) an **independent approver** judges the report; (4) **commit or roll back** -- an allowed command keeps its state and returns its output; a blocked one is rolled back to the snapshot and the reason is returned to the agent. Ships the **YoloFS-Ext** benchmark (102 dangerous tasks where the harm hides inside the tool the agent is asked to run, each with a safe twin), SABER runners, and a Claude Code `PreToolUse` hook mode (needs `bwrap`; Claude Code binary not included). Default model endpoint is OpenRouter-compatible.

Authors' numbers: harmful-outcome rate 6.7% vs >= 14.8% for baselines on SABER, 7.8% vs >= 35.3% on YoloFS-Ext, while blocking 1.0% of the safe twins.

**Revvel hit:** revvel-standards' approval gates (spec-guard, agent-approval-check, hashgate) bind approval to the bytes of a request; Caper adds the other half for commands with side effects: show the approver the observed effects of a dry run, and roll back on refusal. Fits as a pattern inside the existing wr:code / deliver:* step, not a new pipeline. The effects report is reproducible; the LLM approver is not, so a revvel version should gate on deterministic rules over the report (e.g. any credential read or network attempt = hold for human).

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-02 (America/Denver): arXiv abs 200 and PDF/abstract read; GitHub repo API (Apache-2.0, created/pushed dates, 3 stars), LICENSE and README read via API, `claude_code/` tree page 200. Not run (needs Docker + an LLM endpoint). Results are the authors' own; single small repo, two commits, no release or package.

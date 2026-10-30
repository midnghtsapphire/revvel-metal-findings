# flashscript

```json
{
  "id": "flashscript",
  "name": "FlashScript: compiling recurring agent workflows into neuro-symbolic programs",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.33876"
  ],
  "license": "arXiv paper (no code found)",
  "metal": 0,
  "determinism": 4,
  "revvel_hit": "Evidence for compiled-ai: compile a successful recurring run (e.g. a deliver:* routine) into code with parameters, keep LLM calls only where judgment is needed, and review/test the deterministic part separately. Identical tool calls every run in the paper's tests.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-30"
}
```

**FlashScript: Compiling Recurring Agent Workflows into Reusable Neuro-Symbolic Programs** (Sabouri, Hasanbeig, Sage, Sinha, Darling, Tiwari, Garms, Chattopadhyay, Gulwani). arXiv **2610.33876** v1, submitted 2026-10-24 13:32 MDT (cs.HC).

A successful agent run is compiled into a **neuro-symbolic program (NSP)** following a set of guidelines: actions and data transformations become code, instance-specific values become parameters, and only decisions that need model judgment stay as LLM calls (three layers where such calls belong, three techniques to replace most of them with code). The paper is explicit that this localizes nondeterminism rather than removing it, so the code and the remaining model calls can be tested separately. Authors' numbers on 120 WorkBench analytics tasks with Claude Haiku 4.5: NSPs were correct and made **identical tool calls on every run**, with about 70x fewer input tokens and a third of the runtime of a skill-guided agent whose runs varied; on composite tasks the skill-guided agent fell to 23% while NSPs stayed correct and identical; NSPs generalized to all 108 unseen instances of the same templates.

**Revvel hit:** supports **compiled-ai** (rank 2): recurring revvel routines should become code with a few marked model calls, not a fresh agent run each time. Borrow the three-layer rule for where an LLM call is allowed. No new pipeline; applies to routines that already exist.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-30 (America/Denver): arXiv abs 200, export API metadata and abstract read. No code link in the abstract or comment; GitHub search found none. Results are the authors' own, single benchmark and model.

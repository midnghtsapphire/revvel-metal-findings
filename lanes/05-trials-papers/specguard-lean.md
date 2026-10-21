# specguard-lean

```json
{
  "id": "specguard-lean",
  "name": "SpecGuard (Lean 4 task-conflict certificates)",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.09159",
    "https://github.com/prmbiy/specguard"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "pre-wr:code check: before the coder starts, prove the WR description and its tests cannot both be satisfied, so a broken spec is bounced back to spec-approved instead of the agent editing tests or hard-coding outputs",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-21"
}
```

**SpecGuard: Proving a Task Is Broken Before the Agent Cheats** (Param Biyani, MATS; Krishnamurthy Dvijotham, Google DeepMind). arXiv **2610.09159**, submitted 2026-10-06. Code `prmbiy/specguard`, Apache-2.0, created 2026-10-06 13:57 MDT, last push 2026-10-09 01:41 MDT, 1★.

A SpecAgent writes `spec.lean` from the task description and codebase only (it never sees the tests); a TestAgent formalizes the tests into `tests.lean`; a Certifier tries to prove no implementation satisfies both, and when it closes the Lean kernel checks `cert.lean` with `decide`. Verdicts: conflict (certified or execution-evidence only), no-conflict, inconclusive. README numbers on 349 ImpossibleBench-style conflicted SWE-bench tasks: up to 72.8% detected, 51.1% certified, false-negative rate 8.1% vs 39.8% for an LLM judge with full access; about $0.26 per task. The certificate is checkable without trusting the models; whether the formalizations match the task is not proven.

**Revvel hit:** a possible gate between `spec-approved` and `wr:code` for WRs that ship tests with the spec: a certified conflict means the spec goes back, not to the coder. Pairs with **cd-scale-semantic-gap** (schema is not semantics) and **cadence**. Model-generated formalizations, so the verdict is advisory unless a certificate exists.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-21 (America/Denver): arXiv abs + HTML 200 (code link matches), repo API (Apache-2.0), README read raw. Results are the authors' own. Research harness, needs Lean 4 and a frontier model per task; not run.

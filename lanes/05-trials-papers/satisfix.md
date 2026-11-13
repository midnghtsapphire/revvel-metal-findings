# satisfix

```json
{
  "id": "satisfix",
  "name": "SatisFix: surface and recheck specification satisficing before a coding agent writes code",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.16289",
    "https://arxiv.org/html/2611.16289"
  ],
  "license": "paper arXiv; no code repository found",
  "metal": 0,
  "determinism": 2,
  "revvel_hit": "Two-step pre-code prompt for the wr:code stage. Step 1: the coder, cast as an advisor helping revise the task, lists every place it decided a requirement could be handled differently than the spec-approved text says (requirement, chosen implementation, reason). Step 2: it rechecks each listed choice against the spec text and keeps or changes it, then codes. Authors report +5.09% pass@1 on DeepSWE and +7.06% on the SWE-bench Pro hard subset, beating Self-Refine/DeCRIM/ProgCo; dropping the advisor framing loses 6.2%. The step-1 list is also a reviewable artifact to attach to the wr:code handoff.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-13"
}
```

**Eliciting and Mitigating Specification Satisficing in Coding Agents** (arXiv **2611.16289**, Ruixin Wang and Tianyi Zhang, Purdue, submitted 2026-11-12). Defines specification satisficing: the agent considers a choice that meets a requirement, then commits to one that does not, for a reason it finds acceptable, so ordinary self-correction keeps it. SatisFix runs before coding; five LLM backbones, two agent frameworks.

**Revvel hit:** a prompt-only change to the existing wr:code instructions, plus saving the deviation list next to the PR. Measure with the existing deliver:* pass rate on the same items, with and without the step.

**Caution:** a third-party review (pith.science) notes no significance tests and some small per-cell gains (2-6 task flips). Not deterministic by itself; pair with a rule gate.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-13 (America/Denver): arXiv abs page opened (abstract and intro). No code link seen; numbers are the authors'.

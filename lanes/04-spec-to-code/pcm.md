# pcm

```json
{
  "id": "pcm",
  "name": "PCM: Proof-Carrying Messages for agent-to-agent claims",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.39109",
    "https://github.com/Cygnux-Labs/PCM-protocol",
    "https://github.com/Cygnux-Labs/PCM-protocol/blob/main/SPEC.md",
    "https://github.com/Cygnux-Labs/Tracekit",
    "https://pypi.org/project/tracekit-ai/"
  ],
  "license": "MIT (spec, vectors, verifier; Tracekit reference implementation MIT)",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "Rule for the deliver:* handoff: a coder's 'tests passed' or 'approved' only counts as proven when backed by a record the coder could not write (CI run, human approval event); the coder's own report is 'unproven', never 'proven'. Borrow the proven / unproven / failed grading and the conformance vectors; do not adopt the signer or the protocol (0.x draft).",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-30"
}
```

**PCM: A Proof-Carrying Message Protocol for Verifiable Multi-Agent Communication** (Bravish Ghosh). arXiv **2610.39109** v1, submitted 2026-10-28 18:50 MDT (cs.CE); spec, conformance vectors, verifier and benchmark in `Cygnux-Labs/PCM-protocol` (MIT, repo created 2026-10-28, 37 stars at check). Reference implementation is **Tracekit** (`Cygnux-Labs/Tracekit`, MIT; PyPI `tracekit-ai`, latest 1.5.1 uploaded 2026-10-30 06:35 MDT; the README demo pins `tracekit-ai==1.5.0`).

Each claim in an agent's message ("the tests passed", "a person approved this", "I fetched X") can carry evidence: records from an append-only Merkle log written by an **attesting signer** the agent cannot control, with RFC 9162 inclusion proofs. The receiver checks offline and grades each claim **proven / unproven / failed**; a claim resting only on the agent's own report is never proven. Approvals bind to the tool and arguments actually approved (JCS-equal arguments), authority flows as grant chains rooted in a recorded human approval that can only narrow, and replay rules survive restarts. Authors' numbers: on a pre-registered benchmark of 926 messages (712 lies in 16 classes) PCM accepted 10 lies, all stale evidence; plain A2A accepted all 712; two independent verifiers agreed on all verdicts; about 1 ms per check. The repo calls PCM 0.1 experimental (every 0.x may change incompatibly) and the A2A / MCP / HTTP bindings drafts.

**Revvel hit:** this names the gap in a deliver:* handoff where the coder says it ran the tests. Revvel already prefers evidence the agent cannot forge (**attested** receipts bound to the head SHA, **agent-approval-check** human approvals, **spec-guard** hash-bound approval). Borrow the vocabulary and rule: grade each completion claim proven (backed by a CI run / human event record), unproven (agent's word only) or failed, and never let unproven pass the gate. The vectors are a ready KAT if an evidence verifier is ever written. Do not adopt the protocol or signer as a second pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-30 (America/Denver): arXiv abs 200 and export API metadata/abstract; repo page 200 and API (MIT, created 2026-10-28, not a fork); README read; SPEC.md 200; Tracekit repo API (MIT) and PyPI JSON (1.5.1, MIT). Spec not read in full; vectors and benchmark not run. Two days old, single author.

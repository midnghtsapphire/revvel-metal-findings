# Temporal (deterministic workflows)

```json
{
  "id": "temporal",
  "name": "Temporal workflows",
  "lane": "02-formal-replay",
  "status": "watching",
  "urls": [
    "https://docs.temporal.io/workflow-definition"
  ],
  "license": "UNKNOWN (not re-fetched)",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "WR → research → spec-approved → wr:code → CI → ship as one Workflow. LLMs live in Activities.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22"
}
```

Replay from event history. Workflow code must emit the same Command sequence. HTTP and LLMs belong in Activities (not deterministic).

**Revvel hit:** the call chain is already a state machine (`issue-state-machine.yml`, `pr-state-orchestrator.yml`). Temporal is the heavy version of that: Jules/OpenRouter crash → replay, do not fork board state.

**Honesty:** do not stand up Temporal until DST-on-orchestrate.js (TigerBeetle method) proves the label graph is the bug. This is watching, not default infra.

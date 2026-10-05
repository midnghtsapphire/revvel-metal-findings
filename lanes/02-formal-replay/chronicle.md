# chronicle

```json
{
  "id": "chronicle",
  "name": "Chronicle (cut-point replay)",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/theagentplane/chronicle",
    "https://pypi.org/project/agent-chronicle/",
    "https://arxiv.org/abs/2609.20625"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* regressions — record a failed agent run at its LLM/tool/routing boundaries, commit it as a fixture, and replay with one boundary live so the fix is tested in CI with zero model calls",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-05"
}
```

**Chronicle** -- record-and-replay for agent decision graphs. Each marked boundary (LLM call, tool call, routing choice) is captured as an immutable Envelope (OpenTelemetry span shape); a run is a trace committed under `fixtures/traces/`. **Cut-point replay** stubs every upstream boundary from the record and runs exactly one boundary live with new code, turning a recorded incident into a deterministic pytest regression test. Paper (arXiv 2609.20625, submitted 2026-09-17; REALM workshop at EMNLP 2026) reports ~23 µs recording overhead per crossing, zero model calls and bit-stable full replay across 20 runs, and cut-point tests that catch every mutant letting a recorded unsafe action through while a stub-everything baseline catches none. Secret redaction, model-version capture, LangGraph / OpenInference integration. Python ≥3.10; MIT; PyPI `agent-chronicle` **0.5.0** (2026-09-21, schema 2.0 breaking); tip `b9c0630d3df4e63f8b5041778d582140576cad1f`; ~24★.

**Revvel hit:** when a `deliver:*` run misfires (wrong label transition, forbidden tool, bad handoff), freeze that run and commit it as a fixture; the fix PR must pass the cut-point test before merge. Complements **agentape** (process-boundary cassettes, no SDK patch) and **agentverify** (sequence/budget assertions); Chronicle adds the "one boundary live, rest frozen" operation neither has. Python-side only; the Node label-graph path stays on **unflake** / **chronos-dst**.

**Honesty:** CAN-PARTIAL. Verified 2026-10-05 (America/Denver): GitHub live, MIT in pyproject, PyPI 0.5.0 live, arXiv abs live and links this repo. Benchmark is 6 incidents with simulated model boundaries; schema just broke at 0.5.0, so pin the version.

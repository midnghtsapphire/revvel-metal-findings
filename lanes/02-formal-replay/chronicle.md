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
    "https://arxiv.org/abs/2609.20625",
    "https://github.com/theagentplane/chronicle/blob/main/CHANGELOG.md",
    "https://github.com/theagentplane/chronicle/blob/main/docs/migration-0.5-to-1.0.md",
    "https://github.com/theagentplane/control-plane"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* regressions — record a failed agent run at its LLM/tool/routing boundaries, commit it as a fixture, and replay with one boundary live so the fix is tested in CI with zero model calls. Pin agent-chronicle==0.5.0 for the committed-fixture workflow: 1.0 (2026-10-14) removed local stores and committed fixtures and records/replays only through an HTTP control plane",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-05",
  "updated": "2026-10-20"
}
```

**Chronicle** -- record-and-replay for agent decision graphs. Each marked boundary (LLM call, tool call, routing choice) is captured as an immutable Envelope (OpenTelemetry span shape); a run is a trace committed under `fixtures/traces/`. **Cut-point replay** stubs every upstream boundary from the record and runs exactly one boundary live with new code, turning a recorded incident into a deterministic pytest regression test. Paper (arXiv 2609.20625, submitted 2026-09-17; REALM workshop at EMNLP 2026) reports ~23 µs recording overhead per crossing, zero model calls and bit-stable full replay across 20 runs, and cut-point tests that catch every mutant letting a recorded unsafe action through while a stub-everything baseline catches none. Secret redaction, model-version capture, LangGraph / OpenInference integration. Python ≥3.10; MIT; PyPI `agent-chronicle` **0.5.0** (2026-09-21, schema 2.0 breaking); tip `b9c0630d3df4e63f8b5041778d582140576cad1f`; ~24★.

**Revvel hit:** when a `deliver:*` run misfires (wrong label transition, forbidden tool, bad handoff), freeze that run and commit it as a fixture; the fix PR must pass the cut-point test before merge. Complements **agentape** (process-boundary cassettes, no SDK patch) and **agentverify** (sequence/budget assertions); Chronicle adds the "one boundary live, rest frozen" operation neither has. Python-side only; the Node label-graph path stays on **unflake** / **chronos-dst**.

**Honesty:** CAN-PARTIAL. Verified 2026-10-05 (America/Denver): GitHub live, MIT in pyproject, PyPI 0.5.0 live, arXiv abs live and links this repo. Benchmark is 6 incidents with simulated model boundaries; schema just broke at 0.5.0, so pin the version.

**Update 2026-10-20 -- 1.0 is a clean break:** PyPI `agent-chronicle` **1.0.0** (uploaded 2026-10-14 14:16 MDT), **1.1.0** and **1.1.1** (2026-10-15; 1.1.1 only raises a test dependency). Per `CHANGELOG.md` and `docs/migration-0.5-to-1.0.md`: Chronicle is rebuilt on `agentplane-primitives==0.2.*`; **recording is remote only** -- it saves to a control plane over HTTP (`configure(control_plane_url=...)`), and with no URL nothing is delivered; **replay is by `trace_id` + `span_id` read from the control plane**; the JSONL / SQLite / remote stores, the local reference control plane, the CLI and **committed fixtures are removed**, and **0.5 fixtures are not replayable** (re-record). Other breaking changes: kinds are only `llm` / `tool`, `ReplayPlan.live()` → `run()`, a STUB replay of a recorded failure now re-raises (`RecordedCallError`), redaction is opt-in (`configure(default_redactors=True)`), `traceparent` injection is default-deny. The control plane is a separate MIT repo/package (`theagentplane/control-plane`, PyPI `agentplane-control-plane` 1.0.1: one SQLite behind HTTP, 4★).

**Revvel impact:** the "commit the incident under `fixtures/traces/` and replay in CI with zero model calls" story only holds on **0.5.0**. Either pin `agent-chronicle==0.5.0` (schema 2.0, file fixtures) or run the control plane as a service container on the existing CI job and re-record there -- the second adds a stateful service to the replay path. Status stays **active** with the pin; INDEX note updated.

**Honesty (2026-10-20):** CAN-PARTIAL. Verified 2026-10-20 (America/Denver): PyPI JSON (1.1.1 latest; 1.0.0 upload time), commits API (releases #69, #73, #74), raw `CHANGELOG.md` and migration doc on `main`, control-plane repo API (MIT) and PyPI JSON; all three URLs 200. Not run on the box.

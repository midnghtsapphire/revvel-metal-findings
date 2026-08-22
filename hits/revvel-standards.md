# Insertion points in revvel-standards

Do **not** invent a second pipeline. START_HERE_CALL_CHAIN.md wins for what runs next.

## Bottleneck (verified from START_HERE_CALL_CHAIN.md)

Research + WR PR often happen. Coder + `deliver:*` often never.

Missing handoff: apply `wr:code` or `spec-approved`, then `deliver:*`.
Tracked in-repo as the spec-to-action bridge (issue #15507).

## Where a finding may land

| Finding | Touch these, not a new root |
| --- | --- |
| xgrammar-2 | `.github/workflows/openrouter-coder.yml`, `schemas/` (force coder JSON/patches through a grammar), `engines/CONTRACT.md` |
| wasmtime-wit | `engines/` plugin/runner boundary, `engines/CONTRACT.md`, later a WIT world beside `schemas/state.schema.json` |
| tigerbeetle-dst | `scripts/` + a seed-replay harness for `engines/runner-orchestrator/orchestrate.js`; `docs/Master_Inventory/TESTING_STANDARD.md` |

## Already in the SSOT (do not duplicate)

- `docs/Master_Inventory/GOAP_AGENT_STANDARD.md`
- `docs/Master_Inventory/AGENTIC_METHODOLOGY_STANDARD.md`
- `docs/Master_Inventory/AI_RESEARCH_MODULE_STANDARD.md`
- `schemas/state.schema.json`
- `engines/CONTRACT.md`

## Honesty for this map

CAN-PARTIAL: read remotely via public API + raw files. Did not clone. Workflow YAML bodies not fully dumped this scrape.

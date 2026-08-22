# Insertion points in revvel-standards

Do **not** invent a second pipeline. START_HERE_CALL_CHAIN.md wins for what runs next.

## Bottleneck

Research + WR PR often happen. Coder + `deliver:*` often never. Missing handoff: `wr:code` / `spec-approved`, then `deliver:*`. Tracked as spec-to-action bridge (issue #15507).

## Where a finding may land

| Finding | Touch these, not a new root |
| --- | --- |
| xgrammar-2 | `.github/workflows/openrouter-coder.yml`, `schemas/` |
| llama-cpp-gbnf | `schemas/*.gbnf` generated from existing JSON Schema; local engine path |
| wasmtime-wit | `engines/CONTRACT.md`, WIT world beside `schemas/state.schema.json` |
| cranelift | Same as wasmtime: compile step for untrusted/generated runners |
| tigerbeetle-dst | `scripts/` seed-replay for `engines/runner-orchestrator/orchestrate.js`; `TESTING_STANDARD.md` |
| dspy-gepa-mipro | `openrouter-assignee.yml` / research-complete → labeler. Metric lives next to WR history. |

## Already in the SSOT (do not duplicate)

- `docs/Master_Inventory/GOAP_AGENT_STANDARD.md`
- `docs/Master_Inventory/AGENTIC_METHODOLOGY_STANDARD.md`
- `docs/Master_Inventory/AI_RESEARCH_MODULE_STANDARD.md`
- `schemas/state.schema.json`
- `engines/CONTRACT.md`

# Insertion points in revvel-standards

Do **not** invent a second pipeline. START_HERE_CALL_CHAIN.md wins for what runs next.

## The stall, proven

[#15507](https://github.com/midnghtsapphire/revvel-standards/issues/15507) closed completed. Merged payload is a WR essay. `spec-to-action-bridge.yml` and `extract_tasks.py` 404 on main.

## engines/ is tiny

CONTRACT + `orchestrate.js` only. Craft is in `scripts/`.

## Finding → file

| Finding | Touch |
| --- | --- |
| llguidance / xgrammar-2 | OpenRouter structured-output on `openrouter-coder.yml` + `OUTPUT_TYPE` enums |
| llama-cpp-gbnf | `schemas/*.gbnf` + `scripts/local_llm.js` |
| outlines | `scripts/research-engine.js` extractors |
| type-constrained-codegen-pldi-2025 | coder output must typecheck before auto-merge |
| dspy-gepa-mipro | research-complete → wr:code classifier |
| compiled-ai | YAML-spec → four-stage gate on existing `openrouter-coder.yml` + `schemas/`; LLM out of control plane after compile |
| plancompiler | `spec-approved` as CHECK 1–7 over `standards/shapes`; reject unknown primitives |
| extism | mcp-product as signed Wasm; host stays orchestrate.js |
| wasmtime-wit / cranelift | target ABI + lowering |
| tigerbeetle-dst | seed-replay orchestrate.js label graph |
| temporal | watching; after DST |
| openhands | existing fallback only; gate on wr:code |
| colm-2025 | grammar = shape in `standards/shapes/*` |

## Five legal insertion points

1. `engines/<name>/` + register in `orchestrate.js`
2. `schemas/state.schema.json` or sibling `$ref`
3. `standards/` + shapes + one DELIVERY_MATRIX row
4. Handoff labels: consume `research:complete`, emit `wr:code` (the #15507 files)
5. Job on `revvel-engine-spine.yml` or `agent-fallback.yml`

No new `issues: opened` workflow.

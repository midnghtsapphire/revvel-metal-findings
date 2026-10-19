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
| cfgzip | Self-hosted XGrammar path only: preprocess static WR/code GBNF once; wrap existing mask — no second decoder |
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
| agent-approval-check | required `agent-approval-check` status on `main` for deliver:* PRs; `agent_logins` / `excluded_approvers` = `TRUSTED_BOTS` in `trusted-bot-auto-approve.yml`; pin action SHA; needs its own small `pull_request_target` + `issue_comment` workflow, which is outside the five points below, so it needs an owner OK. It is a status-only gate: no issues, no dispatch |
| wassette / act | wasmtime-wit trial host: one helper (e.g. the WR schema checker) as a wasm32-wasip2 component over MCP stdio with operator-written grants; host stays orchestrate.js. **wassette v0.8.1** (2026-10-18) is on Wasmtime 48.0.6, meets the floor, and refuses publisher-bundled OCI policies / ambient env on agent load paths, so it is the host for the trial today. **act** 0.14.6 still locks Wasmtime 49.0.2 (floor >= 49.0.3); use it only after a re-pinned release or `cargo update -p wasmtime` |
| agt-approval-protocol | watching; reference only: shape the deliver:* approval record (action digest over JCS bytes + policy version + chain version, consumed in the same step that starts the side effect) as a sibling `$ref` of `schemas/state.schema.json` (point 2). No AGT runtime. The digest is only as good as the canonicalizer: AGT itself fixed RFC 8785 number formatting on 2026-10-16 (#4341, breaking). Keep numbers integer/string in the record and check the canonicalizer against **agent-evidence-vectors** `vectors-a2a-jcs-v01` (watching; running its Action in CI is a workflow edit, owner OK) |
| agentmachinist | watching; pattern only: `spec-approved` counts only with a bot-minted marker carrying the head SHA after a fail-closed permission read; any push after approval = stale; coder pushes with lease on the approved SHA (point 4, existing labels). Do not adopt the controller |
| gh-actions-lock | `gh actions-lock` over the existing `.github/workflows/` (openrouter-coder.yml, revvel-engine-spine.yml, agent-fallback.yml, trusted-bot-auto-approve.yml) → commit `.github/workflows/actions.lock`; add `gh actions-lock --verify` as one step on an existing job (point 5). Locks the runner side the replay lane cannot see. Edits revvel-standards workflow files, so it needs an owner OK; no new workflow, no dispatch |
| vllm-batch-invariance / vosti | self-hosted coder only (not OpenRouter): before any live re-run diff of a wr:code replay, run Vosti's four bitwise-logit checks (batch, chunked prefill, prefill vs decode, prefix reuse) on the exact model + backend + `vllm==0.32.0` you serve, as one step on an existing job (point 5). Vosti found vLLM's batch-invariant mode mismatching on Gemma3-4B, so determinism is per model, not a flag. No new workflow |

## Five legal insertion points

1. `engines/<name>/` + register in `orchestrate.js`
2. `schemas/state.schema.json` or sibling `$ref`
3. `standards/` + shapes + one DELIVERY_MATRIX row
4. Handoff labels: consume `research:complete`, emit `wr:code` (the #15507 files)
5. Job on `revvel-engine-spine.yml` or `agent-fallback.yml`

No new `issues: opened` workflow.

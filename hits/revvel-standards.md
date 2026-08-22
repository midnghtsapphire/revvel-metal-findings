# Insertion points in revvel-standards

Do **not** invent a second pipeline. START_HERE_CALL_CHAIN.md wins for what runs next. MASTER.md wins process conflicts.

Mapped remotely 2026-08-22. No clone.

## The stall, proven

Issue [#15507](https://github.com/midnghtsapphire/revvel-standards/issues/15507) asked for a kickoff when `research:complete` lands: extract DoD, emit a task list, apply `wr:code` or `wr:jules`, stuck-detect. Closed `completed` 2026-07-09 via [PR #15572](https://github.com/midnghtsapphire/revvel-standards/pull/15572).

What actually merged: `wr/issues/issue-15507-spec-to-action-bridge-research-completes-execution.md` (another WR essay). Proposed `.github/workflows/spec-to-action-bridge.yml` and `scripts/extract_tasks.py` **do not exist** on `main` (404 this scrape). Source note `wr/pending/03-spec-to-action-bridge.md` is still pending.

The bridge issue died of the disease it was written to cure.

## engines/ is tiny

```
engines/CONTRACT.md
engines/runner-orchestrator/README.md
engines/runner-orchestrator/orchestrate.js   # npm run engine; Ajv vs state.schema.json
```

Craft work lives in `scripts/` (`research-engine.js`, `local_llm.js`, `stuck-wr-detector.js`, `bnatsheaf/`). Workflows are ignition only.

## Already deterministic in-repo (do not duplicate)

- `engines/CONTRACT.md` + `schemas/state.schema.json` + Ajv on every write
- `schemas/agent-contract.schema.json` (Grid/Block/Thread → `agent-fallback.yml`)
- `standards/DELIVERY_MATRIX.md` + `standards/shapes/*` + `OUTPUT_TYPE_TO_CHANNEL`
- `standards/DECISION_SCORING_ENGINE_STANDARD.md`
- `standards/GOAP_SWARM_RULES.md`, `GOAP.md`, `GOAP_AGENT_PROMPT.md`, `docs/Master_Inventory/GOAP_AGENT_STANDARD.md`, `products/goap-swarm-console/lib/goap-engine.js`
- `scripts/bnatsheaf/`, `scripts/local_llm.js`, `scripts/llm-spend-gate.js`
- `.github/workflows/revvel-engine-spine.yml` (additive wrap of `npm run engine`)
- `.github/workflows/spec-approval-gate.yml` (label half of the missing handoff)

## Five legal insertion points

1. **`engines/<name>/` + register in `orchestrate.js`**  
   Return `{ artifacts[], next_engine, runner_calls[], bom?, status }` per CONTRACT. No new orchestrator.

2. **`schemas/state.schema.json` or a sibling `$ref`**  
   Rule 3: every write validates. Same pattern as `agent-contract.schema.json`.

3. **`standards/<NEW>_STANDARD.md` + `standards/shapes/<SHAPE>.md` + one row in DELIVERY_MATRIX**  
   Extend `OUTPUT_TYPE_TO_CHANNEL`. Do not invent a new ship workflow.

4. **Handoff labels, not a new intake**  
   Consume `wr:research-complete` / `research:complete`, emit `wr:code` | `spec-approved`, later `deliver:*`. Touch `research-engine.yml`, `spec-approval-gate.yml`, `openrouter-coder.yml`. This is #15507's actual missing files.

5. **Job on `revvel-engine-spine.yml` or `agent-fallback.yml`**  
   New `kind` / `runner_target` enum. Then one line in START_HERE step table + SYSTEM_MAP. Spine is already marked additive.

Do **not** add another `issues: opened` workflow.

## Bottleneck files (touch these)

| Path | Why |
| --- | --- |
| `.github/workflows/openrouter-coder.yml` | Dead until `wr:code` or `spec-approved` |
| `.github/workflows/spec-approval-gate.yml` | Other half of the label bridge |
| `.github/workflows/ship-to-market.yml` | Needs `deliver:*` on merged PR |
| `engines/runner-orchestrator/orchestrate.js` | Maps output_type → deliver, but is the *optional* local spine |
| `scripts/research-engine.js` | Multi-LLM fan-out on every WR open |
| `.github/workflows/pr-state-orchestrator.yml` | Merge gravity before ship |

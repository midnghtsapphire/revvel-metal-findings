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
| wassette / act | wasmtime-wit trial host: one helper (e.g. the WR schema checker) as a wasm32-wasip2 component over MCP stdio with operator-written grants; host stays orchestrate.js. **Trial on hold (2026-10-20):** the Wasmtime floor moved to **>= 48.0.7 / 49.0.4** on 2026-10-19 (critical aarch64 Cranelift sandbox escape GHSA-mghf-wjfp-p5xm). **wassette v0.8.1** is on 48.0.6 and its open dependabot bump (#895) only reaches 49.0.3; **act** 0.14.6 still locks 49.0.2. Run neither until a release pins >= 48.0.7 / 49.0.4, or build from source after `cargo update -p wasmtime --precise <patched>`. wassette remains the preferred host (refuses publisher-bundled OCI policies / ambient env on agent load paths) |
| agt-approval-protocol | watching; reference only: shape the deliver:* approval record (action digest over JCS bytes + policy version + chain version, consumed in the same step that starts the side effect) as a sibling `$ref` of `schemas/state.schema.json` (point 2). No AGT runtime. The digest is only as good as the canonicalizer: AGT itself fixed RFC 8785 number formatting on 2026-10-16 (#4341, breaking). Keep numbers integer/string in the record and check the canonicalizer against **agent-evidence-vectors** `vectors-a2a-jcs-v01` (watching; running its Action in CI is a workflow edit, owner OK) |
| agentmachinist | watching; pattern only: `spec-approved` counts only with a bot-minted marker carrying the head SHA after a fail-closed permission read; any push after approval = stale; coder pushes with lease on the approved SHA (point 4, existing labels). Do not adopt the controller |
| gh-actions-lock | `gh actions-lock` over the existing `.github/workflows/` (openrouter-coder.yml, revvel-engine-spine.yml, agent-fallback.yml, trusted-bot-auto-approve.yml) → commit `.github/workflows/actions.lock`; add `gh actions-lock --verify` as one step on an existing job (point 5). Locks the runner side the replay lane cannot see. Edits revvel-standards workflow files, so it needs an owner OK; no new workflow, no dispatch |
| vllm-batch-invariance / vosti | self-hosted coder only (not OpenRouter): before any live re-run diff of a wr:code replay, run Vosti's four bitwise-logit checks (batch, chunked prefill, prefill vs decode, prefix reuse) on the exact model + backend + `vllm==0.32.0` you serve, as one step on an existing job (point 5). Vosti found vLLM's batch-invariant mode mismatching on Gemma3-4B, so determinism is per model, not a flag. No new workflow |
| attested | watching; deliver:* merge side, evidence half: a Sigstore-signed (`actions/attest`) in-toto receipt of the repo's own test run bound to the PR head SHA, checked by a required `attested verify` status that runs from the default branch and never executes PR code; fails closed on no receipt / wrong signer workflow / SHA mismatch / FAILED. Sits beside agent-approval-check on the required-checks list. Would be `attested run` + sign + verify on an existing job (point 5) plus a repository-ruleset entry (user-owned repo, so only the weaker check-name form). Workflow + ruleset edit: owner OK. Pin `Praxso/attested@<full sha>` via gh-actions-lock. No second pipeline |
| chronicle | replay lane note (2026-10-20): the committed-fixture flow (`fixtures/traces/` replayed in CI with zero model calls) needs `agent-chronicle==0.5.0`; 1.x records/replays only via an HTTP control plane. Do not unpin without deciding to run that service in the CI job |
| leanguard / mcp-destructive-approval | watching; reference for the deliver:* tool-call rule set (point 1 engine, point 2 record): deny unless permitted, history rules (tests observed after last edit; spec-approved observed before deliver:*), approval bound to exact arguments + a state revision and single-use; on the coder's MCP path hold every tool not annotated read-only / non-destructive in the gateway, never via a model-settable flag. LeanGuard is an RC (v0.2.0-rc2, not on PyPI): borrow the shape, no runtime yet |
| gated-sdd-audit / delegated-scope / eval-instrument | watching; three checks, no new pipeline: (1) the declared-files / undeclared-change diff against the spec-approved file list runs as a CI job that fails the deliver:* PR, never as an instruction the coder's orchestrator judges itself (arXiv 2611.05094: self-run check stopped work in 4 of 11 flagged blocks); (2) each deliver:* coder's MCP allowlist lists only actions on its own WR's repo/branch/issue, enforced by the existing gate (mcp-gate / mcp-hangar), not an LLM judge (arXiv 2611.04086); (3) any required check that scores runs reports its graded fraction and pins its evaluator version, so an ungraded run can never read as pass or fail (arXiv 2611.04399). |
| germline-exec / agenttrustci / torve 0.8.0 | watching; no new pipeline: (1) per-call data scope for the deliver:* coder's MCP tools, enforced in the existing mcp-hangar / verax gate (germline-exec); (2) deterministic trace assertions (allowed tools, order, claims match tool output) as a job on `revvel-engine-spine.yml` (agenttrustci idea); (3) the deliver:* gate convicts only tests red at head and not red on the merge base (torve `@suite` rule) |
| se-agent-failure-prediction / continuous-benchmarks / reprobridge / agentverify 0.9.0 | watching; no new pipeline: (1) do not gate wr:code stop/retry on a mid-run trajectory failure classifier — issue difficulty alone beats it (se-agent-failure-prediction); (2) continuous oracle + human-gated repair for fleet evals beside eval-instrument (continuous-benchmarks); (3) deliver:* packet should carry refined procedures/env/launchers, not raw code alone (reprobridge shape); (4) agentverify pin stays ==0.7.1; 0.9.0 is the upgrade target only with fixed tool-call ids and `max_age` unset |
| detent / caleta / untrusted-model-agentsec / replay-fidelity-appworld / xgrammar 0.2.9 / mcp-hangar 2.36.3 | watching; no new pipeline: (1) self-hosted coder only: batch-invariant serving is now ~1.04-1.17x Stock cost (Detent, no code yet), so bit-exact wr:code replay stops being a latency argument; (2) `scripts/local_llm.js`: refuse to start on a model whose size/SHA-256 differs from a committed manifest, log a prompt-free record per run (Caleta pattern); (3) existing deliver:* gate (mcp-hangar / verax): capability-bound per-WR allowlist plus a deterministic approval budget per run (untrusted-model-agentsec); (4) fixture replay: reset RNG per interaction and compare side-effect state, not printed output (replay-fidelity-appworld); (5) bump xgrammar floor to >= 0.2.9 where self-hosted and mcp-hangar stdio pin to ==2.36.3 |
| flowplan / activesecharness / agency-harness / sfu-sim / mcp-hangar 2.36.4 | watching; no new pipeline: (1) wr:code coder records its intended change as typed graph deltas and a deliver:* job compares them with the rebuilt CFG/DFG, a completion bit that replaces re-reading/re-testing (FlowPlan, 0.32-0.76x tokens, authors); (2) log tokens and LLM calls per wr:code run as the baseline for any harness trim (Agency, up to 35% cost cut); (3) deliver:* guard stays deterministic with per-WR capability tokens and trust x sensitivity taint, never an LLM judge (ActiveSecHarness); (4) self-hosted only: SFU-Sim is the bit-exact reference for cross-GPU drift; (5) mcp-hangar stdio pin may move to ==2.36.4 |
| infer-determinism / nbxgrammar / expertcrowd-swe / mcp-hangar 2.36.6 | watching; no new pipeline: (1) add an inert change and a lazy patch as control cases to the existing deliver:* gate tests, both must fail (ExpertCrowd-SWE grader calibration); (2) spec-approved schema check refuses unknown JSON Schema keywords by name instead of ignoring them (nbxgrammar); (3) self-hosted only: infer-determinism is the acceptance test before trusting batch-invariant serving; (4) mcp-hangar stdio pin moves to ==2.36.6 so a server or group removed from the config file cannot come back after a restart |

## Five legal insertion points

1. `engines/<name>/` + register in `orchestrate.js`
2. `schemas/state.schema.json` or sibling `$ref`
3. `standards/` + shapes + one DELIVERY_MATRIX row
4. Handoff labels: consume `research:complete`, emit `wr:code` (the #15507 files)
5. Job on `revvel-engine-spine.yml` or `agent-fallback.yml`

No new `issues: opened` workflow.

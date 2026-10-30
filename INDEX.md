# INDEX

Ranked by bang-for-buck on `revvel-standards` as of scrape `2026-10-30`.

| rank | id | lane | status | why |
| ---: | --- | --- | --- | --- |
| 0 | issue-15507-closed-as-essay | 04-spec-to-code | active | Bridge WR closed as a WR. Target. |
| 1 | gh-aw-safe-outputs | 04-spec-to-code | active | Safe label/PR apply without agent write tokens. |
| 2 | compiled-ai | 04-spec-to-code | active | Compile WR once; LLM out of the control plane. |
| 3 | spec-guard | 04-spec-to-code | active | Hash-bound human Approve/Authorize/Complete; MCP refuses skip. |
| 4 | plancompiler | 05-trials-papers | active | Seven static checks = spec-approved before emit. |
| 5 | agent-spec | 04-spec-to-code | active | Rust intent compiler: REQ IR → Task Contracts → lifecycle/guard. |
| 6 | specd | 04-spec-to-code | active | Compile specs into coder context; verify plan before implement. |
| 7 | contract-agent | 04-spec-to-code | active | Spec-as-Source CEL guards refuse illegal tool/multi-turn transitions. |
| 8 | governspec | 04-spec-to-code | active | One govern.yaml → tool artifacts + offline acceptance tests (MIT). |
| 9 | aicontracts | 04-spec-to-code | active | Fail-closed YAML effects + CI check-verdict for deliver:* coder. |
| 10 | homi-gate | 04-spec-to-code | active | CI completion bit + handoff contract + MCP allowlist for deliver:*. |
| 11 | agent-approval-check | 04-spec-to-code | active | Merge-side gate: agent-authored PRs need N write-access human approvals (SHA-bound `/approve`); bot approvals never count; fail-closed (MIT, Anthropic). |
| 12 | agent-gate | 04-spec-to-code | active | MCP fail-closed ship checklist + hash-chained receipts. |
| 13 | verax | 04-spec-to-code | active | MCP policy gate + signed COSE decision/effect ledger; pin >= 0.8.0 (held calls bound to the hash of the forwarded arguments; approve/retry/ledger/reconcile compare it, unbound rows refused); keep keys outside the state dir; 0.7.0 / 0.6.1 / 0.5.x fixes still apply. |
| 14 | mcp-gate | 04-spec-to-code | active | Fail-closed stdio MCP proxy for the coder: policy-denied tool calls never reach the server; Ed25519-signed chained receipts (Apache-2.0). |
| 15 | agentgate | 04-spec-to-code | active | Commit `agentgate.lock` of the coder's MCP tool surface; `ci` exits 1 on description/schema drift; `deps` flags hallucinated/typosquat packages (Apache-2.0); test the lock against **mcp-digest-vectors**. |
| 16 | cadence | 04-spec-to-code | active | Node/TS settle gate: refuses "done" until declared ACs re-check from real evidence; 1.71.0/1.72.0 record review/audit and forced Stop-gate bypasses so a forced settle can't grade `strong`; 1.72.0 stops handoff deleting git-tracked docs -- pin >= 1.72.0 (MIT). |
| 17 | gh-actions-lock | 02-formal-replay | active | GitHub-official `actions.lock`: existing wr:code/deliver:* workflows run the exact action commits you locked even if tags move; `--verify` fails CI on drift. v0.3.0 shipped the impostor-commit fix (#186, breaking verify); **v0.4.0** (2026-10-23) is non-breaking (docs: `--verify-local` is coverage only; GHE.com auth); start on v0.4.0 or v0.3.0. **Lockfiles GA on the platform 2026-10-28 (Dependabot updates lockfile in the same PR; Require lockfile policy GA)**; extension still pre-1.0 (MIT). Install only `github/gh-actions-lock` (33 look-alike repos). Needs owner OK to touch workflows. |
| 18 | llguidance | 01-deterministic-ai | active | Vendor structured-output path you already pay for. |
| 19 | xgrammar-2 | 01-deterministic-ai | active | Serving-engine mask (vLLM/SGLang); pin >= 0.2.6 (2026-10-04 advisories); vLLM 0.32.0 ships 0.2.8. |
| 20 | cfgzip | 01-deterministic-ai | active | Lossless vocab compression over XGrammar2 for complex static grammars. |
| 21 | grammar-sparse-projection | 01-deterministic-ai | active | Triton sparse LM-head from XGrammar masks; exact support; research path. |
| 22 | pre3 | 01-deterministic-ai | active | LightLLM DPDA mask; ACL Outstanding. |
| 23 | psc | 05-trials-papers | active | Next mask engine if self-hosting (~700x claims); now peer-reviewed ISSTA 2026. |
| 24 | glrmask | 01-deterministic-ai | active | Live Rust/Py mask lib, also Node-API (`@glrmask/node`) + C/C++; **0.5.0 published 2026-10-26, breaking again** (commit_forced_tokens, EBNF and markers removed, special tokens via extern, exclusive C/C++ ranges, MSRV 1.89) after 0.4.0's new Grammar/Module/Constraint API; keep ==0.3.1, any port goes straight to ==0.5.0; paper claims p99 9.54 µs vs llguidance 379.6 µs (Zenodo preprint). |
| 25 | gramr | 01-deterministic-ai | active | Rust JSON-Schema->PDA token masks; property-tested; local schema twin. |
| 26 | vocab-mask-trie | 01-deterministic-ai | active | Zero-dep TS byte-trie vocab mask for local Node coder. |
| 27 | static-constraint-decoding | 01-deterministic-ai | active | YouTube STATIC sparse-trie for closed-set deliver:* allowlists. |
| 28 | trie-automata | 05-trials-papers | watching | Amazon large-K enum trie; claimed vLLM LogitsProcessor 29x; code pending. |
| 29 | truncproof | 05-trials-papers | active | JSON + hard token budget -- kill truncated WR dumps. |
| 30 | chopchop | 05-trials-papers | active | Semantic AST pruners beyond CFG/types for wr:code. |
| 31 | swyb | 05-trials-papers | active | Distance-to-accept for general CFGs under budget. |
| 32 | crane-icml-2025 | 01-deterministic-ai | active | CoT free, final answer constrained. |
| 33 | type-constrained-codegen-pldi-2025 | 05-trials-papers | active | Type mask for the JS/TS coder path. |
| 34 | cd-scale-semantic-gap | 05-trials-papers | active | CD guarantees schema not semantics; keep behavioral gates. |
| 35 | unflake | 02-formal-replay | active | Shrink + exhaustive Node DST for label-graph async races. |
| 36 | chronos-dst | 02-formal-replay | active | Node/TS seed-replay with network/entropy capsules. |
| 37 | agentverify | 02-formal-replay | active | pytest cassette replay for tool sequences/budgets/forbidden tools; 0.7.x replays recorded tool results and fails stale cassettes with a diff -- pin ==0.7.1. 0.8.0 (breaking) adds `assert_tool_calls_allowed` but random per-run tool-call ids and wall-clock cassette expiry: only with fixed ids and `max_age` unset. |
| 38 | agentape | 02-formal-replay | active | Process-boundary HTTP/MCP cassette wrap; no SDK patch. |
| 39 | chronicle | 02-formal-replay | active | Cut-point replay: recorded incident becomes a CI regression test, no live LLM. Pin `==0.5.0`: 1.0 dropped committed fixtures for a remote control plane. |
| 40 | llama-cpp-gbnf | 01-deterministic-ai | active | Local twin. |
| 41 | outlines | 01-deterministic-ai | active | Python cage on research-engine dumps. |
| 42 | dspy-gepa-mipro | 04-spec-to-code | active | Compile the labeler. |
| 43 | extism | 00-near-metal | active | Signed Wasm plugins now; WIT later; BSD-3-Clause, 1.41.0 takes `wasmtime ^49` (lock >= 49.0.5). |
| 44 | wasmtime-wit | 00-near-metal | active | Target ABI (+ Pulley portable interp); 50.0.0 final (CLI drops WASIp0 by default); **floor >= 50.0.1 or >= 49.0.5 / 48.0.8 / 36.0.20** (2026-10-29: component resource-transfer memory bug, wasi-sockets UDP bypass + 3 low). |
| 45 | wassette | 00-near-metal | active | Microsoft Wasm-Component-over-MCP host, deny-by-default per-component grants; v0.8.1 on Wasmtime 48.0.6, **below the 48.0.8 / 49.0.5 floor** -- hold the trial; rejects publisher-bundled OCI policies, no env/secrets without a policy; early development (MIT). |
| 46 | act | 00-near-metal | active | Wasm Component tools over MCP with declared-capability + explicit grants, headless = deny, always-on audit; 0.14.6 still locks Wasmtime 49.0.2, three patches below the 49.0.5 floor -- re-pin before trial (MIT OR Apache-2.0). |
| 47 | cranelift | 00-near-metal | active | Lowering. |
| 48 | tigerbeetle-dst | 02-formal-replay | active | Seed-replay method (Zig-native reference). |
| 49 | colm-2025-correctness-guaranteed-decode | 05-trials-papers | active | Grammar = public API. |
| 50 | agentassert-abc | 04-spec-to-code | watching | MCP tool-call guard + ABC contracts; AGPL — prefer MIT contract-agent. |
| 51 | hlv | 04-spec-to-code | watching | Rust SDD proof binary + MCP; prefer agent-spec for wire. |
| 52 | specgate | 04-spec-to-code | watching | Approve exact spec version, hand coder a governed Context Pack, submit delivery evidence vs ACs; heavy Go+Python stack, model-judged gates. |
| 53 | schoolmarm | 01-deterministic-ai | watching | Zero-dep pure-Rust GBNF mask (llama.cpp port) for a Rust/Wasm host. |
| 54 | vllm-batch-invariance | 01-deterministic-ai | watching | `VLLM_BATCH_INVARIANT=1`: self-hosted coder output independent of batch size/order; vLLM 0.32.0 incl. ROCm; AWQ-on-sm8x #59086 closed (fixed on main), GPTQ #60479 open; still beta, #39096 open; DSv4.1 bitwise BI PR #62365 open; qualify per model (Vosti). |
| 55 | deepinfer | 01-deterministic-ai | watching | DeepSeek production engine (Apache-2.0, 2026-10-20): `DEEPINFER_BATCH_INVARIANT=1` + `DEEPINFER_ENABLE_MTP_VARLEN=0` + fixed `seq_seed` = deterministic sampling, plus regex/JSON-Schema/EBNF outputs; NVIDIA SM100 / Ascend 950, one model -- reference recipe only. |
| 56 | concordance | 01-deterministic-ai | watching | Deterministic model, nondeterministic pipeline: per-run ids, unordered lists and growing registries in prompts changed results 4 of 4 runs on a 800/800 bit-stable SGLang server; stdlib `compare_runs.py` finds the first diverging stage from captured calls (Apache-2.0, 1 day old). Rule now: nothing per-run in a wr:code prompt. |
| 57 | vosti | 05-trials-papers | watching | Verus + Z3-verified deterministic inference engine (bitwise logits across batch/chunk/prefill-decode/prefix reuse); borrow its 4-axis logit test to qualify any self-hosted replay; single-GPU research prototype (MIT). |
| 58 | bitexact-llm | 01-deterministic-ai | watching | Integer (fixed-point) Llama-3.2-1B engine: same int64 logits + tokens across H800/H100/x86/M4 CPU and batch/KV schedules, int8 vLLM 0.32.0 plugin; research prototype, 1B only, ~0.28x vLLM throughput (Apache-2.0). New replay experiment: stock vLLM re-sampled only 13–17% of flagged failures token-for-token vs 100% with BitExact. Borrow the record/compare logits-hash report for any replay. |
| 59 | dispinv | 01-deterministic-ai | watching | Batch invariance on Hopper by pinning cuBLAS/FA3/Inductor dispatch, fails closed (exit 70) when a pin is not live, `PROOF` log lines, fault-injection negative control (Apache-2.0, 2026-10-30, one commit, vLLM main `36768d1`, SM90 only, monkeypatches); borrow the qualify-before-trust pattern only. |
| 60 | determinate | 03-agent-runtimes | watching | State-gated next-action + constrained structured output. |
| 61 | openhands | 03-agent-runtimes | watching | Fallback coder. Gate on wr:code. |
| 62 | temporal | 02-formal-replay | watching | Heavy replay. After DST proves the bug. |
| 63 | agrepl | 02-formal-replay | watching | Go static-binary MITM record/replay, zero outbound network on replay; any language, no SDK; CI mode still on roadmap. |
| 64 | tracely | 02-formal-replay | watching | Fail-to-pass replay cases from failing agent traces, replayed offline as a PR gate (MIT, repo 2026-10-11, SDK 0.0.1); borrow the case contract only, platform (ClickHouse/Postgres/Redis/MinIO, open dev auth, Action @master) would be a second pipeline. |
| 65 | zig-0-16 | 00-near-metal | watching | Guest language, not default. |
| 66 | qbe | 00-near-metal | watching | Teachable IR only. |
| 67 | agt-approval-protocol | 04-spec-to-code | watching | Microsoft AGT ADR-0030 (accepted): approval bound to JCS SHA-256 action digest + policy/chain version; consume in the execute transaction; timeout/unauth = deny; LLM advisory only (MIT); #4341 fixed RFC 8785 float formatting (breaking digest), still unreleased. |
| 68 | agent-evidence-vectors | 02-formal-replay | watching | Known-answer conformance corpora + Action for evidence verifiers: RFC 8785 a2a-jcs canonicalizer vectors, receipt/ledger tamper cases, occurrence-binding, approval-binding (v0.26.0, 23 cases = KATs for the spec-approved gate); v0.27.0/v0.28.0 add dispatch-fence, converted-argument-binding, authority-at-dispatch and Proof-of-Control corpora (approved call = dispatched call); v0.29.x adds completion-confirmation (did the deliver:* call actually land) and delegator-right corpora. **0.29.1's wheel/sdist missed a signed corpus; v0.29.2 (2026-10-28) ships it plus a wheel-vs-signed-list SHA-256 gate (borrow for deliver:* artifacts); v0.29.3 adds an OT corpus (out of scope); v0.30.0 (2026-10-29) adds an uncertain-effect corpus (write committed, reply lost: retry must not double-apply) + loopback runtime harness.** Keep ==0.24.0 existing corpora; ==0.26.1 approval-binding; ==0.28.0 dispatch-fence; **==0.29.2 (or ==0.29.3) for completion-confirmation / delegator-right, never ==0.29.1**; ==0.30.0 for uncertain-effect, after a diff (Apache-2.0); CI step needs owner OK. |
| 69 | mcp-digest-vectors | 02-formal-replay | watching | 45 before/after `tools/list` vectors + known-answer digests (RFC 8785 + SHA-256, full tool object; draft scheme for MCP SEP-3452): KAT for agentgate.lock / mcp-hangar pins; reject duplicate keys, description-only pins miss 8 of 18 drifts (MIT, 2026-10-29, no release -- pin a commit SHA). |
| 70 | attested | 04-spec-to-code | watching | Sigstore-signed in-toto test receipt bound to the PR head SHA + fail-closed `attested verify` required check run from the default branch: deliver:* proof tests ran green on that exact SHA (Apache-2.0, npm 0.1.0); main fix #44 (`allow-unsigned` no longer passes a failed fork run) -- pin a main SHA >= `7bf6181` if adopted; workflow + ruleset edit needs owner OK. |
| 71 | pcm | 04-spec-to-code | watching | Proof-Carrying Messages (arXiv 2610.39109, MIT spec + vectors + verifier): a claim like "tests passed" / "approved" is proven only by a record the agent can't write; agent's own word = unproven, never proven (10 of 712 lies accepted, authors' numbers). Borrow the proven/unproven/failed rule for deliver:*; 0.x draft, don't adopt. |
| 72 | spec-growth-engine | 04-spec-to-code | watching | Model-free drift floor: SPEC.md graph per node, import-graph drift blocks undeclared deps, "verified" only from recorded passing tests voided by the next change; pre-commit hook (Apache-2.0, 2★, no releases). Borrow layer 1 only; layer 2 is a second agent pipeline. |
| 73 | torve | 04-spec-to-code | watching | Spec-and-gate engine (MIT, alpha, 0.7.0 2026-10-27): `gates run --base` exit-code gates (`scope` globs, `no-test-tampering`, `red-on-base`, `acceptance`) + `gates check` sabotage suite proving each gate can fail; LOCKED/ASSUMED/OPEN decision grades. Borrow the gate layer only; its planner/sandbox loop would be a second pipeline. |
| 74 | specguard-lean | 05-trials-papers | watching | Lean 4 certificate that a task description and its tests cannot both hold, before the coder starts (arXiv 2610.09159, Apache-2.0); bounce broken WRs back to spec-approved; model-built formalizations. |
| 75 | who-verifies-builder | 05-trials-papers | watching | Paper (arXiv 2610.28667, 2026-10-16; artifact MIT): Verification Contract written from the spec, fresh-context verifier beats builder's own tests (p = 0.006), other-vendor verifier adds nothing; human release decision. Shape for spec-approved → deliver:*. |
| 76 | skeleton-coding | 05-trials-papers | watching | Paper (arXiv 2610.38214, 2026-10-27): tests alone underdetermine the program; a code-like skeleton (types/modules/signatures) in the spec cut test error 48.4% and cost 15-26x (authors' numbers). spec-approved could ship a skeleton with the ACs; no code. |
| 77 | flashscript | 05-trials-papers | watching | Paper (arXiv 2610.33876, 2026-10-24, Gulwani et al.): compile a recurring agent run into code + parameters + a few marked LLM calls; identical tool calls every run, ~70x fewer input tokens (authors' numbers). Evidence for compiled-ai; no code. |
| 78 | bi-acceptance-gates | 05-trials-papers | watching | Paper (arXiv 2610.36623, 2026-10-26): batch-invariance as successive acceptance gates in an agent's kernel loop (static contract check, then bitwise replay across batch contexts, then benchmark); 19 of 83 released kernels violated BI; pass rate 67.6% to 91.9% keeping 91.8% of speedup. Pattern only, no code released. |
| 79 | corun | 05-trials-papers | watching | Paper (arXiv 2608.14376, 2026-08): deterministic inference by scheduling (isolated prefill + fixed-shape CUDA-graph decode), 15-324% throughput over batch-invariant kernels; no code found. Only if self-hosting the coder. |
| 80 | agentmachinist | 04-spec-to-code | watching | Spec→Approve→Execute controller: bot-minted SHA marker after fail-closed write-permission read; label alone = pending; push = stale; lease push on approved SHA (MIT, PyPI 0.20.0); pattern only, own pipeline. |
| 81 | hashgate | 04-spec-to-code | watching | Claude Code PreToolUse: hash-bound push/merge/deploy; server re-derives live state; agent cannot self-approve (Apache-2.0, PyPI 0.2.0, stale since 2026-07). |
| 82 | notary-mcp | 04-spec-to-code | watching | MCP propose→canonicalize→approve revision hash→fail-closed execute exact bytes (MIT); demo/hackathon; borrow pattern only. |
| 83 | mcpgate | 04-spec-to-code | watching | Go deny-by-default MCP proxy, human `ask` queue, audit-failure denies; backup to mcp-gate (MIT). |
| 84 | mcp-gatehouse | 04-spec-to-code | watching | In-server Python MCP approval tiers; no approver = deny (MIT). 0.4.0 needs `mcp>=2,<3`; **set mcp>=2.2.0 and opt in to `validate_token_resource` (MCP Python SDK advisories 2026-10-27, CVE-2026-116684/5/6).** |
| 85 | mcp-hangar | 04-spec-to-code | watching | Fleet MCP enforcement plane; tool-schema digest pin fails closed, `pin --check` exits 1; drifted tools withheld; 2.34.2 fixed silent pin bypasses; 2.34.4 binds discovery approvals to the full definition SHA-256; 2.34.7 needs fpdf2>=2.8.8 for `full`; **2.34.8 (2026-10-30) stops group views leaking every member to every tenant** -- pin ==2.34.8 (==2.34.7 ok single-tenant), never below 2.34.2, no 2.34.6 (MIT); runtime twin of agentgate. |
| 86 | swiftgram | 05-trials-papers | watching | ASE 2026 grammar-constrained decoding via lexical forking; no code yet. |
| 87 | linebreak-gate | 04-spec-to-code | dropped | DROPPED 2026-10-12: repo 404, all PyPI releases yanked, now licensed product. Use spec-guard. |

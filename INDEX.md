# INDEX

Ranked by bang-for-buck on `revvel-standards` as of scrape `2026-10-20`.

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
| 13 | verax | 04-spec-to-code | active | MCP policy gate + signed COSE decision/effect ledger; pin >= 0.6.1 (operator-text escaping, signed downstream tool pins, reconcile reads signed amounts only); 0.5.x fail-closed parsing still applies. |
| 14 | mcp-gate | 04-spec-to-code | active | Fail-closed stdio MCP proxy for the coder: policy-denied tool calls never reach the server; Ed25519-signed chained receipts (Apache-2.0). |
| 15 | agentgate | 04-spec-to-code | active | Commit `agentgate.lock` of the coder's MCP tool surface; `ci` exits 1 on description/schema drift; `deps` flags hallucinated/typosquat packages (Apache-2.0). |
| 16 | cadence | 04-spec-to-code | active | Node/TS settle gate: refuses "done" until declared ACs re-check from real evidence; pin >= 1.69.1 (MCP SDK advisory) (MIT). |
| 17 | gh-actions-lock | 02-formal-replay | active | GitHub-official `actions.lock`: existing wr:code/deliver:* workflows run the exact action commits you locked even if tags move; `--verify` fails CI on drift; Free plan preview, pre-1.0 (MIT). Install only `github/gh-actions-lock` (33 look-alike repos). Needs owner OK to touch workflows. |
| 18 | llguidance | 01-deterministic-ai | active | Vendor structured-output path you already pay for. |
| 19 | xgrammar-2 | 01-deterministic-ai | active | Serving-engine mask (vLLM/SGLang); pin >= 0.2.6 (2026-10-04 advisories); vLLM 0.32.0 ships 0.2.8. |
| 20 | cfgzip | 01-deterministic-ai | active | Lossless vocab compression over XGrammar2 for complex static grammars. |
| 21 | grammar-sparse-projection | 01-deterministic-ai | active | Triton sparse LM-head from XGrammar masks; exact support; research path. |
| 22 | pre3 | 01-deterministic-ai | active | LightLLM DPDA mask; ACL Outstanding. |
| 23 | psc | 05-trials-papers | active | Next mask engine if self-hosting (~700x claims); now peer-reviewed ISSTA 2026. |
| 24 | glrmask | 01-deterministic-ai | active | Live Rust/Py mask lib, also Node-API (`@glrmask/node`) + C/C++; pin ==0.3.1 (0.4.0 RC on main is breaking again, unpublished); paper claims p99 9.54 µs vs llguidance 379.6 µs (Zenodo preprint). |
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
| 37 | agentverify | 02-formal-replay | active | pytest cassette replay for tool sequences/budgets/forbidden tools; pin >= 0.5.0 (unreplayable calls now raise instead of hitting the live API; creds redacted). |
| 38 | agentape | 02-formal-replay | active | Process-boundary HTTP/MCP cassette wrap; no SDK patch. |
| 39 | chronicle | 02-formal-replay | active | Cut-point replay: recorded incident becomes a CI regression test, no live LLM. Pin `==0.5.0`: 1.0 dropped committed fixtures for a remote control plane. |
| 40 | llama-cpp-gbnf | 01-deterministic-ai | active | Local twin. |
| 41 | outlines | 01-deterministic-ai | active | Python cage on research-engine dumps. |
| 42 | dspy-gepa-mipro | 04-spec-to-code | active | Compile the labeler. |
| 43 | extism | 00-near-metal | active | Signed Wasm plugins now; WIT later; BSD-3-Clause, 1.41.0 takes `wasmtime ^49` (lock >= 49.0.4). |
| 44 | wasmtime-wit | 00-near-metal | active | Target ABI (+ Pulley portable interp); pin hosts >= 49.0.4 / 48.0.7 (2026-10-19: critical aarch64 Cranelift `br_table` sandbox escape + wasi-http fixes). |
| 45 | wassette | 00-near-metal | active | Microsoft Wasm-Component-over-MCP host, deny-by-default per-component grants; v0.8.1 on Wasmtime 48.0.6, **below the new 48.0.7 / 49.0.4 floor** (dependabot #895 → 49.0.3 also short) -- hold the trial; rejects publisher-bundled OCI policies, no env/secrets without a policy; early development (MIT). |
| 46 | act | 00-near-metal | active | Wasm Component tools over MCP with declared-capability + explicit grants, headless = deny, always-on audit; 0.14.6 still locks Wasmtime 49.0.2, two patches below the 49.0.4 floor -- re-pin before trial (MIT OR Apache-2.0). |
| 47 | cranelift | 00-near-metal | active | Lowering. |
| 48 | tigerbeetle-dst | 02-formal-replay | active | Seed-replay method (Zig-native reference). |
| 49 | colm-2025-correctness-guaranteed-decode | 05-trials-papers | active | Grammar = public API. |
| 50 | agentassert-abc | 04-spec-to-code | watching | MCP tool-call guard + ABC contracts; AGPL — prefer MIT contract-agent. |
| 51 | hlv | 04-spec-to-code | watching | Rust SDD proof binary + MCP; prefer agent-spec for wire. |
| 52 | specgate | 04-spec-to-code | watching | Approve exact spec version, hand coder a governed Context Pack, submit delivery evidence vs ACs; heavy Go+Python stack, model-judged gates. |
| 53 | schoolmarm | 01-deterministic-ai | watching | Zero-dep pure-Rust GBNF mask (llama.cpp port) for a Rust/Wasm host. |
| 54 | vllm-batch-invariance | 01-deterministic-ai | watching | `VLLM_BATCH_INVARIANT=1`: self-hosted coder output independent of batch size/order; vLLM 0.32.0 incl. ROCm; AWQ-on-sm8x #59086 closed (fixed on main), GPTQ #60479 open; still beta, #39096 open; qualify per model (Vosti). |
| 55 | vosti | 05-trials-papers | watching | Verus + Z3-verified deterministic inference engine (bitwise logits across batch/chunk/prefill-decode/prefix reuse); borrow its 4-axis logit test to qualify any self-hosted replay; single-GPU research prototype (MIT). |
| 56 | determinate | 03-agent-runtimes | watching | State-gated next-action + constrained structured output. |
| 57 | openhands | 03-agent-runtimes | watching | Fallback coder. Gate on wr:code. |
| 58 | temporal | 02-formal-replay | watching | Heavy replay. After DST proves the bug. |
| 59 | agrepl | 02-formal-replay | watching | Go static-binary MITM record/replay, zero outbound network on replay; any language, no SDK; CI mode still on roadmap. |
| 60 | zig-0-16 | 00-near-metal | watching | Guest language, not default. |
| 61 | qbe | 00-near-metal | watching | Teachable IR only. |
| 62 | agt-approval-protocol | 04-spec-to-code | watching | Microsoft AGT ADR-0030 (accepted): approval bound to JCS SHA-256 action digest + policy/chain version; consume in the execute transaction; timeout/unauth = deny; LLM advisory only (MIT); #4341 fixed RFC 8785 float formatting (breaking digest), still unreleased. |
| 63 | agent-evidence-vectors | 02-formal-replay | watching | Known-answer conformance corpora + Action for evidence verifiers: RFC 8785 a2a-jcs canonicalizer vectors, receipt/ledger tamper cases, occurrence-binding (one approval, one execution); pin ==0.24.0 (Apache-2.0); CI step needs owner OK. |
| 64 | attested | 04-spec-to-code | watching | Sigstore-signed in-toto test receipt bound to the PR head SHA + fail-closed `attested verify` required check run from the default branch: deliver:* proof tests ran green on that exact SHA (Apache-2.0, npm 0.1.0, 6 days old); workflow + ruleset edit needs owner OK. |
| 65 | agentmachinist | 04-spec-to-code | watching | Spec→Approve→Execute controller: bot-minted SHA marker after fail-closed write-permission read; label alone = pending; push = stale; lease push on approved SHA (MIT, PyPI 0.20.0); pattern only, own pipeline. |
| 66 | hashgate | 04-spec-to-code | watching | Claude Code PreToolUse: hash-bound push/merge/deploy; server re-derives live state; agent cannot self-approve (Apache-2.0, PyPI 0.2.0, stale since 2026-07). |
| 67 | notary-mcp | 04-spec-to-code | watching | MCP propose→canonicalize→approve revision hash→fail-closed execute exact bytes (MIT); demo/hackathon; borrow pattern only. |
| 68 | mcpgate | 04-spec-to-code | watching | Go deny-by-default MCP proxy, human `ask` queue, audit-failure denies; backup to mcp-gate (MIT). |
| 69 | mcp-gatehouse | 04-spec-to-code | watching | In-server Python MCP approval tiers; no approver = deny (MIT). |
| 70 | mcp-hangar | 04-spec-to-code | watching | Fleet MCP enforcement plane; tool-schema digest pin fails closed, `pin --check` exits 1; 2.30.0 withholds drifted tools; 2.31.0 `mcp-hangar approvals` approve/deny CLI resolves held stdio calls via the same CAS/expiry chokepoint (MIT); runtime twin of agentgate. |
| 71 | swiftgram | 05-trials-papers | watching | ASE 2026 grammar-constrained decoding via lexical forking; no code yet. |
| 72 | linebreak-gate | 04-spec-to-code | dropped | DROPPED 2026-10-12: repo 404, all PyPI releases yanked, now licensed product. Use spec-guard. |

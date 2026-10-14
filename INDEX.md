# INDEX

Ranked by bang-for-buck on `revvel-standards` as of scrape `2026-10-14`.

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
| 13 | verax | 04-spec-to-code | active | MCP policy gate + signed COSE decision/effect ledger; pin >= 0.5.1 (stricter fail-closed policy parsing). |
| 14 | mcp-gate | 04-spec-to-code | active | Fail-closed stdio MCP proxy for the coder: policy-denied tool calls never reach the server; Ed25519-signed chained receipts (Apache-2.0). |
| 15 | agentgate | 04-spec-to-code | active | Commit `agentgate.lock` of the coder's MCP tool surface; `ci` exits 1 on description/schema drift; `deps` flags hallucinated/typosquat packages (Apache-2.0). |
| 16 | cadence | 04-spec-to-code | active | Node/TS settle gate: refuses "done" until declared ACs re-check from real evidence; pin >= 1.69.1 (MCP SDK advisory) (MIT). |
| 17 | llguidance | 01-deterministic-ai | active | Vendor structured-output path you already pay for. |
| 18 | xgrammar-2 | 01-deterministic-ai | active | Serving-engine mask (vLLM/SGLang); pin >= 0.2.6 (2026-10-04 advisories). |
| 19 | cfgzip | 01-deterministic-ai | active | Lossless vocab compression over XGrammar2 for complex static grammars. |
| 20 | grammar-sparse-projection | 01-deterministic-ai | active | Triton sparse LM-head from XGrammar masks; exact support; research path. |
| 21 | pre3 | 01-deterministic-ai | active | LightLLM DPDA mask; ACL Outstanding. |
| 22 | psc | 05-trials-papers | active | Next mask engine if self-hosting (~700x claims); now peer-reviewed ISSTA 2026. |
| 23 | glrmask | 01-deterministic-ai | active | Live Rust/Py mask lib; 0.2.0 breaking API (pin ==0.2.0, rebuild artifacts); interim MaskBench tails beat LLGuidance claims. |
| 24 | gramr | 01-deterministic-ai | active | Rust JSON-Schema->PDA token masks; property-tested; local schema twin. |
| 25 | vocab-mask-trie | 01-deterministic-ai | active | Zero-dep TS byte-trie vocab mask for local Node coder. |
| 26 | static-constraint-decoding | 01-deterministic-ai | active | YouTube STATIC sparse-trie for closed-set deliver:* allowlists. |
| 27 | trie-automata | 05-trials-papers | watching | Amazon large-K enum trie; claimed vLLM LogitsProcessor 29x; code pending. |
| 28 | truncproof | 05-trials-papers | active | JSON + hard token budget -- kill truncated WR dumps. |
| 29 | chopchop | 05-trials-papers | active | Semantic AST pruners beyond CFG/types for wr:code. |
| 30 | swyb | 05-trials-papers | active | Distance-to-accept for general CFGs under budget. |
| 31 | crane-icml-2025 | 01-deterministic-ai | active | CoT free, final answer constrained. |
| 32 | type-constrained-codegen-pldi-2025 | 05-trials-papers | active | Type mask for the JS/TS coder path. |
| 33 | cd-scale-semantic-gap | 05-trials-papers | active | CD guarantees schema not semantics; keep behavioral gates. |
| 34 | unflake | 02-formal-replay | active | Shrink + exhaustive Node DST for label-graph async races. |
| 35 | chronos-dst | 02-formal-replay | active | Node/TS seed-replay with network/entropy capsules. |
| 36 | agentverify | 02-formal-replay | active | pytest cassette replay for tool sequences/budgets/forbidden tools. |
| 37 | agentape | 02-formal-replay | active | Process-boundary HTTP/MCP cassette wrap; no SDK patch. |
| 38 | chronicle | 02-formal-replay | active | Cut-point replay: recorded incident becomes a CI regression test, no live LLM. |
| 39 | llama-cpp-gbnf | 01-deterministic-ai | active | Local twin. |
| 40 | outlines | 01-deterministic-ai | active | Python cage on research-engine dumps. |
| 41 | dspy-gepa-mipro | 04-spec-to-code | active | Compile the labeler. |
| 42 | extism | 00-near-metal | active | Signed Wasm plugins now; WIT later. |
| 43 | wasmtime-wit | 00-near-metal | active | Target ABI (+ Pulley portable interp); pin hosts >= 49.0.2 (security). |
| 44 | act | 00-near-metal | active | Wasm Component tools over MCP with declared-capability + explicit grants, headless = deny, always-on audit; already on Wasmtime 49.0.2 (MIT OR Apache-2.0). |
| 45 | cranelift | 00-near-metal | active | Lowering. |
| 46 | tigerbeetle-dst | 02-formal-replay | active | Seed-replay method (Zig-native reference). |
| 47 | colm-2025-correctness-guaranteed-decode | 05-trials-papers | active | Grammar = public API. |
| 48 | agentassert-abc | 04-spec-to-code | watching | MCP tool-call guard + ABC contracts; AGPL — prefer MIT contract-agent. |
| 49 | hlv | 04-spec-to-code | watching | Rust SDD proof binary + MCP; prefer agent-spec for wire. |
| 50 | specgate | 04-spec-to-code | watching | Approve exact spec version, hand coder a governed Context Pack, submit delivery evidence vs ACs; heavy Go+Python stack, model-judged gates. |
| 51 | schoolmarm | 01-deterministic-ai | watching | Zero-dep pure-Rust GBNF mask (llama.cpp port) for a Rust/Wasm host. |
| 52 | vllm-batch-invariance | 01-deterministic-ai | watching | `VLLM_BATCH_INVARIANT=1`: self-hosted coder output independent of batch size/order; beta, SM<90 + torch.compile hole (#39096). |
| 53 | determinate | 03-agent-runtimes | watching | State-gated next-action + constrained structured output. |
| 54 | openhands | 03-agent-runtimes | watching | Fallback coder. Gate on wr:code. |
| 55 | temporal | 02-formal-replay | watching | Heavy replay. After DST proves the bug. |
| 56 | agrepl | 02-formal-replay | watching | Go static-binary MITM record/replay, zero outbound network on replay; any language, no SDK; CI mode still on roadmap. |
| 57 | wassette | 00-near-metal | watching | Microsoft Wasm-Component-over-MCP host, deny-by-default per-component grants; blocked until it ships Wasmtime >= 48.0.5/49.0.2 (MIT). |
| 58 | zig-0-16 | 00-near-metal | watching | Guest language, not default. |
| 59 | qbe | 00-near-metal | watching | Teachable IR only. |
| 60 | hashgate | 04-spec-to-code | watching | Claude Code PreToolUse: hash-bound push/merge/deploy; server re-derives live state; agent cannot self-approve (Apache-2.0, PyPI 0.2.0, stale since 2026-07). |
| 61 | notary-mcp | 04-spec-to-code | watching | MCP propose→canonicalize→approve revision hash→fail-closed execute exact bytes (MIT); demo/hackathon; borrow pattern only. |
| 62 | mcpgate | 04-spec-to-code | watching | Go deny-by-default MCP proxy, human `ask` queue, audit-failure denies; backup to mcp-gate (MIT). |
| 63 | mcp-gatehouse | 04-spec-to-code | watching | In-server Python MCP approval tiers; no approver = deny (MIT). |
| 64 | mcp-hangar | 04-spec-to-code | watching | Fleet MCP enforcement plane; tool-schema digest pin fails closed, `pin --check` exits 1; pin 2.27.5 (MIT); runtime twin of agentgate. |
| 65 | swiftgram | 05-trials-papers | watching | ASE 2026 grammar-constrained decoding via lexical forking; no code yet. |
| 66 | linebreak-gate | 04-spec-to-code | dropped | DROPPED 2026-10-12: repo 404, all PyPI releases yanked, now licensed product. Use spec-guard. |

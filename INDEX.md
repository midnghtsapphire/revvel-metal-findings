# INDEX

Ranked by bang-for-buck on `revvel-standards` as of scrape `2026-10-06`.

| rank | id | lane | status | why |
| ---: | --- | --- | --- | --- |
| 0 | issue-15507-closed-as-essay | 04-spec-to-code | active | Bridge WR closed as a WR. Target. |
| 1 | gh-aw-safe-outputs | 04-spec-to-code | active | Safe label/PR apply without agent write tokens. |
| 2 | compiled-ai | 04-spec-to-code | active | Compile WR once; LLM out of the control plane. |
| 3 | spec-guard | 04-spec-to-code | active | Hash-bound human Approve/Authorize/Complete; MCP refuses skip. |
| 4 | linebreak-gate | 04-spec-to-code | active | Human-approved acceptance criteria over MCP; fail-closed CI check until sign-off. |
| 5 | plancompiler | 05-trials-papers | active | Seven static checks = spec-approved before emit. |
| 6 | agent-spec | 04-spec-to-code | active | Rust intent compiler: REQ IR → Task Contracts → lifecycle/guard. |
| 7 | specd | 04-spec-to-code | active | Compile specs into coder context; verify plan before implement. |
| 8 | contract-agent | 04-spec-to-code | active | Spec-as-Source CEL guards refuse illegal tool/multi-turn transitions. |
| 9 | governspec | 04-spec-to-code | active | One govern.yaml → tool artifacts + offline acceptance tests (MIT). |
| 10 | aicontracts | 04-spec-to-code | active | Fail-closed YAML effects + CI check-verdict for deliver:* coder. |
| 11 | homi-gate | 04-spec-to-code | active | CI completion bit + handoff contract + MCP allowlist for deliver:*. |
| 12 | agent-gate | 04-spec-to-code | active | MCP fail-closed ship checklist + hash-chained receipts. |
| 13 | verax | 04-spec-to-code | active | MCP policy gate + signed COSE decision/effect ledger. |
| 14 | cadence | 04-spec-to-code | active | Node/TS settle gate: refuses "done" until declared ACs re-check from real evidence (MIT). |
| 15 | llguidance | 01-deterministic-ai | active | Vendor structured-output path you already pay for. |
| 16 | xgrammar-2 | 01-deterministic-ai | active | Serving-engine mask (vLLM/SGLang). |
| 17 | cfgzip | 01-deterministic-ai | active | Lossless vocab compression over XGrammar2 for complex static grammars. |
| 18 | grammar-sparse-projection | 01-deterministic-ai | active | Triton sparse LM-head from XGrammar masks; exact support; research path. |
| 19 | pre3 | 01-deterministic-ai | active | LightLLM DPDA mask; ACL Outstanding. |
| 20 | psc | 05-trials-papers | active | Next mask engine if self-hosting (~700x claims); now peer-reviewed ISSTA 2026. |
| 21 | glrmask | 01-deterministic-ai | active | Live Rust/Py mask lib; MaskBench TBM tails beat LLGuidance claims. |
| 22 | gramr | 01-deterministic-ai | active | Rust JSON-Schema->PDA token masks; property-tested; local schema twin. |
| 23 | vocab-mask-trie | 01-deterministic-ai | active | Zero-dep TS byte-trie vocab mask for local Node coder. |
| 24 | static-constraint-decoding | 01-deterministic-ai | active | YouTube STATIC sparse-trie for closed-set deliver:* allowlists. |
| 25 | trie-automata | 05-trials-papers | watching | Amazon large-K enum trie; claimed vLLM LogitsProcessor 29x; code pending. |
| 26 | truncproof | 05-trials-papers | active | JSON + hard token budget -- kill truncated WR dumps. |
| 27 | chopchop | 05-trials-papers | active | Semantic AST pruners beyond CFG/types for wr:code. |
| 28 | swyb | 05-trials-papers | active | Distance-to-accept for general CFGs under budget. |
| 29 | crane-icml-2025 | 01-deterministic-ai | active | CoT free, final answer constrained. |
| 30 | type-constrained-codegen-pldi-2025 | 05-trials-papers | active | Type mask for the JS/TS coder path. |
| 31 | cd-scale-semantic-gap | 05-trials-papers | active | CD guarantees schema not semantics; keep behavioral gates. |
| 32 | unflake | 02-formal-replay | active | Shrink + exhaustive Node DST for label-graph async races. |
| 33 | chronos-dst | 02-formal-replay | active | Node/TS seed-replay with network/entropy capsules. |
| 34 | agentverify | 02-formal-replay | active | pytest cassette replay for tool sequences/budgets/forbidden tools. |
| 35 | agentape | 02-formal-replay | active | Process-boundary HTTP/MCP cassette wrap; no SDK patch. |
| 36 | chronicle | 02-formal-replay | active | Cut-point replay: recorded incident becomes a CI regression test, no live LLM. |
| 37 | llama-cpp-gbnf | 01-deterministic-ai | active | Local twin. |
| 38 | outlines | 01-deterministic-ai | active | Python cage on research-engine dumps. |
| 39 | dspy-gepa-mipro | 04-spec-to-code | active | Compile the labeler. |
| 40 | extism | 00-near-metal | active | Signed Wasm plugins now; WIT later. |
| 41 | wasmtime-wit | 00-near-metal | active | Target ABI (+ Pulley portable interp); pin hosts >= 49.0.2 (security). |
| 42 | cranelift | 00-near-metal | active | Lowering. |
| 43 | tigerbeetle-dst | 02-formal-replay | active | Seed-replay method (Zig-native reference). |
| 44 | colm-2025-correctness-guaranteed-decode | 05-trials-papers | active | Grammar = public API. |
| 45 | agentassert-abc | 04-spec-to-code | watching | MCP tool-call guard + ABC contracts; AGPL — prefer MIT contract-agent. |
| 46 | hlv | 04-spec-to-code | watching | Rust SDD proof binary + MCP; prefer agent-spec for wire. |
| 47 | schoolmarm | 01-deterministic-ai | watching | Zero-dep pure-Rust GBNF mask (llama.cpp port) for a Rust/Wasm host. |
| 48 | determinate | 03-agent-runtimes | watching | State-gated next-action + constrained structured output. |
| 49 | openhands | 03-agent-runtimes | watching | Fallback coder. Gate on wr:code. |
| 50 | temporal | 02-formal-replay | watching | Heavy replay. After DST proves the bug. |
| 51 | zig-0-16 | 00-near-metal | watching | Guest language, not default. |
| 52 | qbe | 00-near-metal | watching | Teachable IR only. |

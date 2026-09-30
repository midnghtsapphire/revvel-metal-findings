# INDEX

Ranked by bang-for-buck on `revvel-standards` as of scrape `2026-09-30`.

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
| 9 | llguidance | 01-deterministic-ai | active | Vendor structured-output path you already pay for. |
| 10 | xgrammar-2 | 01-deterministic-ai | active | Serving-engine mask (vLLM/SGLang). |
| 11 | cfgzip | 01-deterministic-ai | active | Lossless vocab compression over XGrammar2 for complex static grammars. |
| 12 | grammar-sparse-projection | 01-deterministic-ai | active | Triton sparse LM-head from XGrammar masks; exact support; research path. |
| 13 | pre3 | 01-deterministic-ai | active | LightLLM DPDA mask; ACL Outstanding. |
| 14 | psc | 05-trials-papers | active | Next mask engine if self-hosting (~700x vs LLGuidance claims). |
| 15 | glrmask | 01-deterministic-ai | active | Live Rust/Py mask lib; MaskBench TBM tails beat LLGuidance claims. |
| 16 | gramr | 01-deterministic-ai | active | Rust JSON-Schema->PDA token masks; property-tested; local schema twin. |
| 17 | vocab-mask-trie | 01-deterministic-ai | active | Zero-dep TS byte-trie vocab mask for local Node coder. |
| 18 | static-constraint-decoding | 01-deterministic-ai | active | YouTube STATIC sparse-trie for closed-set deliver:* allowlists. |
| 19 | trie-automata | 05-trials-papers | watching | Amazon large-K enum trie; claimed vLLM LogitsProcessor 29x; code pending. |
| 20 | truncproof | 05-trials-papers | active | JSON + hard token budget -- kill truncated WR dumps. |
| 21 | chopchop | 05-trials-papers | active | Semantic AST pruners beyond CFG/types for wr:code. |
| 22 | swyb | 05-trials-papers | active | Distance-to-accept for general CFGs under budget. |
| 23 | crane-icml-2025 | 01-deterministic-ai | active | CoT free, final answer constrained. |
| 24 | type-constrained-codegen-pldi-2025 | 05-trials-papers | active | Type mask for the JS/TS coder path. |
| 25 | cd-scale-semantic-gap | 05-trials-papers | active | CD guarantees schema not semantics; keep behavioral gates. |
| 26 | unflake | 02-formal-replay | active | Shrink + exhaustive Node DST for label-graph async races. |
| 27 | chronos-dst | 02-formal-replay | active | Node/TS seed-replay with network/entropy capsules. |
| 28 | agentverify | 02-formal-replay | active | pytest cassette replay for tool sequences/budgets/forbidden tools. |
| 29 | llama-cpp-gbnf | 01-deterministic-ai | active | Local twin. |
| 30 | outlines | 01-deterministic-ai | active | Python cage on research-engine dumps. |
| 31 | dspy-gepa-mipro | 04-spec-to-code | active | Compile the labeler. |
| 32 | extism | 00-near-metal | active | Signed Wasm plugins now; WIT later. |
| 33 | wasmtime-wit | 00-near-metal | active | Target ABI (+ Pulley portable interp). |
| 34 | cranelift | 00-near-metal | active | Lowering. |
| 35 | tigerbeetle-dst | 02-formal-replay | active | Seed-replay method (Zig-native reference). |
| 36 | colm-2025-correctness-guaranteed-decode | 05-trials-papers | active | Grammar = public API. |
| 37 | agentassert-abc | 04-spec-to-code | watching | MCP tool-call guard + ABC contracts; AGPL — prefer MIT contract-agent. |
| 38 | hlv | 04-spec-to-code | watching | Rust SDD proof binary + MCP; prefer agent-spec for wire. |
| 39 | determinate | 03-agent-runtimes | watching | State-gated next-action + constrained structured output. |
| 40 | openhands | 03-agent-runtimes | watching | Fallback coder. Gate on wr:code. |
| 41 | temporal | 02-formal-replay | watching | Heavy replay. After DST proves the bug. |
| 42 | zig-0-16 | 00-near-metal | watching | Guest language, not default. |
| 43 | qbe | 00-near-metal | watching | Teachable IR only. |

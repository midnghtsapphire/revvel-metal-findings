# schoolmarm

```json
{
  "id": "schoolmarm",
  "name": "SchoolMarm",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/Michael-A-Kuykendall/schoolmarm",
    "https://crates.io/crates/schoolmarm"
  ],
  "license": "MIT OR Apache-2.0",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Local twin in Rust: GBNF grammar + vocab → per-step allowed-token bitmask with zero deps and no unsafe, so a Rust/Wasm host can mask coder output without linking llama.cpp C++",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-06"
}
```

**SchoolMarm** -- GBNF grammar-constrained decoding as a pure-Rust leaf crate: zero dependencies, no `unsafe`. Given a GBNF grammar string and a token vocabulary it returns the allowed-token mask at each step (`GrammarState::allowed_tokens`, `accept_token`, `is_accepting`). Clean-room port of llama.cpp's `llama-grammar.cpp` algorithms (recursive-descent GBNF parser, nondeterministic pushdown stack, character-level token matching), aiming for full GBNF compatibility. crates.io **0.1.1** (published 2026-03-03, ~3.4k downloads); repo tip `b914ff356a91bee98aa8e95ae4d94d231d32ac62` (2026-08-26, docs only); ~4★.

**Revvel hit:** same grammars as **llama-cpp-gbnf**, but embeddable in a Rust or `wasm32-wasip2` component host (see **wasmtime-wit**) with no C++ toolchain, so one GBNF file can drive both the llama.cpp twin and an in-process mask. Not a serving-engine backend; for throughput stay on **xgrammar-2** / **llguidance** / **glrmask**.

**Honesty:** CAN-PARTIAL. Verified 2026-10-06 (America/Denver): GitHub live, crates.io 0.1.1 live, Cargo.toml declares MIT OR Apache-2.0 (no LICENSE file at repo root; raw `/LICENSE` 404). No crate release since March and no published benchmarks; per-step cost is a character-level NPDA walk over the whole vocab, so expect it to be slow on 100k+ vocabularies. Watching until it either gets a release with a token-trie fast path or proves itself in a trial.

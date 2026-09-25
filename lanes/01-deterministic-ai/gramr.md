# gramr

```json
{
  "id": "gramr",
  "name": "gramr",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/PDiTO/gramr"
  ],
  "license": "MIT",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Rust JSON-Schema->PDA token masks for wr:code / deliver:* structured packets -- local schema-bound coder path without inventing a second engine",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-25"
}
```

**gramr** -- Rust constrained-decoding library. Compiles a JSON Schema into a byte-level pushdown automaton (per-rule DFAs + call edges), builds a vocabulary trie, and at every step returns a `BitSet` of allowed tokenizer tokens so sampled output always validates. Closest design cousin to XGrammar (accepted / rejected / stack-dependent token split + cached per-state index). Supports objects/arrays/enums/`anyOf`/`oneOf` (disjoint)/`$ref` recursion/`pattern` subset/numeric bounds; rejects left-recursion and unbounded whitespace padding. Property tests (proptest) prove: random walks validate with `serde_json` + `jsonschema`; valid docs are accepted; fast mask == brute-force; no dead ends; `rollback(n)` restores mask. Criterion benches on `cl100k_base` (~1-2 us warm mask). Demo binary samples from noise and still emits valid JSON. MIT; `Cargo.toml` `version = "0.1.0"`; created 2026-09-25.

**Revvel hit:** pin WR / `deliver:*` JSON schemas (tool-call envelopes, order packets, label graphs) through `Grammar::from_json_schema` + `Matcher::allowed_tokens` on the local Node/Rust coder twin -- schema is the contract, mask is the gate. Pair with **llguidance** / **xgrammar-2** on the serving path; gramr is the teachable / embeddable Rust masker when you do not want a full serving-engine dependency. Do **not** stand up a parallel inference stack.

**Honesty:** CAN-PARTIAL. Verified 2026-09-25 (America/Denver): GitHub `PDiTO/gramr` live (0*, MIT LICENSE, Rust 2024 / rust-version 1.88, created 2026-09-25T11:23:58Z); tree has `src/{automaton,schema,grammar,index,matcher,trie,vocab,bitset}.rs`, `tests/` (schema_features / matcher / properties), `benches/`, `examples/schemas/{person,order,tool_call,tree}.json`, CI under `.github`. **Not on crates.io** yet (README: path/git dep only). **No vLLM / SGLang / llama.cpp plugin** -- library + demo sampler only. Stars 0 / brand-new; metal is the automaton + property suite, not adoption.

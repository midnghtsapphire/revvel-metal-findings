# vocab-mask-trie

```json
{
  "id": "vocab-mask-trie",
  "name": "vocab-mask-trie",
  "lane": "01-deterministic-ai",
  "status": "active",
  "urls": [
    "https://github.com/nradawg/vocab-mask-trie"
  ],
  "license": "MIT",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Zero-dep TypeScript byte-trie vocab mask from a character grammar — local Node twin for schema-valid wr:code dumps when the coder is not on vLLM/XGrammar",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-18"
}
```

TypeScript library that compiles a character-level grammar into a **byte-level** automaton, then builds legal next-token sets by jointly walking that automaton with a vocabulary trie. Correctly classifies fused multi-terminal tokens and mid-UTF-8 token bytes (refuses string vocabularies at the API). API: `compileVocabMask` → `allowed(state)` / `toByteMask()` / `advance(state, tokenId)`. Liveness = completable (backward reachability from accept). Finite automaton only: recursion rejected; bounded nesting via `repeat`. Zero runtime dependencies; `package.json` names `vocab-mask-trie@0.1.0`; **not published to npm** this scrape (registry 404).

**Revvel hit:** when a local / Node research coder needs hard next-token masks for WR JSON without pulling Python/Rust (GLRMask) or a serving backend (XGrammar/llguidance), this is the cleanest TS mask primitive found. Keep vendor/vLLM paths on llguidance/XGrammar — swap only the local mask engine behind the existing coder contract.

**Honesty:** CAN-PARTIAL. GitHub `nradawg/vocab-mask-trie` + MIT LICENSE verified live 2026-09-18. 0★; created 2026-08-16; not on npm yet. FSM ≠ full CFG/PDA (no unbounded nesting). No vLLM / SGLang / llama.cpp plugin. Companion repo `nradawg/mask-state-rollback` (journaled trial-feed for rejected candidates; linear vocab scan; also unpublished) noted in scrape log, not catalogued separately.

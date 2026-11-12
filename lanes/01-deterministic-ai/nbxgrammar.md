# nbxgrammar

```json
{
  "id": "nbxgrammar",
  "name": "nbxgrammar: std-only Rust JSON-Schema/tool-call grammar engine with C ABI",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/NeuroBrix/nbxgrammar",
    "https://pypi.org/project/nbxgrammar/"
  ],
  "license": "Apache-2.0 (contributions under a NeuroBrix CAA)",
  "metal": 4,
  "determinism": 5,
  "revvel_hit": "Fail-closed schema compile: any JSON Schema keyword it cannot enforce is refused by name (ValueError), never silently ignored, which is the property a spec-approved packet schema needs (no quiet loosening). Rust std only, ctypes from Python, oracle tests check every mask against brute force over the vocabulary. Author numbers on Qwen3 vocab (M4 Pro): ~15 us median mask inside JSON, ~92 us median per step on the bench. Only matters for a self-hosted coder; for OpenRouter, borrow the refuse-unknown-keyword rule in the existing schema check.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-12"
}
```

**nbxgrammar** (`NeuroBrix/nbxgrammar`, Apache-2.0, created 2026-11-10; PyPI `nbxgrammar` 0.1.1). Compiles a JSON Schema subset or a tool-call format description to a token-mask matcher; engine behind NeuroBrix's `response_format: json_schema` and forced `tool_choice`. Whitespace is canonical (at most one space, no newlines), so the same schema gives a narrower output space. Pinned Rust toolchain; functions capped at 53 lines in CI.

**Revvel hit:** the refuse-unsupported-keyword behavior is worth copying into the spec-approved packet schema check today (insertion point: the existing schema validation step, no new pipeline). The engine itself is a local twin to gramr / glrmask only if a coder is self-hosted.

**Honesty:** CAN-PARTIAL, watching (one day old, 1 star, single vendor). Verified 2026-11-12 (America/Denver): GitHub API (Apache-2.0); README read; PyPI JSON (0.1.1, license field empty). Not run; latency numbers are the author's.

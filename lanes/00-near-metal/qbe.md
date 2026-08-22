# QBE

```json
{
  "id": "qbe",
  "name": "QBE",
  "lane": "00-near-metal",
  "status": "watching",
  "urls": [
    "https://c9x.me/compile/"
  ],
  "license": "UNKNOWN",
  "metal": 5,
  "determinism": 5,
  "revvel_hit": "Low. Teachable SSA IL only if a WR needs an IR, not the default coder path.",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Tiny SSA IL + C ABI. amd64 / arm64 / riscv64. Their line: most of industrial opts in a small compiler.

**Revvel hit:** low. Cranelift is the production IR we already paired with Wasmtime. Keep QBE as a teaching artifact, not a runner.

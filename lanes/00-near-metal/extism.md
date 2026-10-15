# Extism

```json
{
  "id": "extism",
  "name": "Extism",
  "lane": "00-near-metal",
  "status": "active",
  "urls": [
    "https://extism.org/",
    "https://github.com/extism/extism",
    "https://extism.org/docs/overview",
    "https://github.com/extism/extism/releases/tag/v1.41.0"
  ],
  "license": "BSD-3-Clause",
  "metal": 4,
  "determinism": 3,
  "revvel_hit": "mcp-product / control-plane tools as signed Wasm + XTP schema, not more Node",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22",
  "updated": "2026-10-15"
}
```

Live Wasm plugin host + PDKs (Rust/JS/Python/Go/Zig/…). XTP: schema → plugin bindgen. Host-gated HTTP. Not the full WASI Component Model.

Several 2026 hosts are moving Extism → native Wasmtime+WIT. Extism still wins when you need a PDK today.

**Revvel hit:** `OUTPUT_TYPE=mcp-product` as a signed `.wasm` with the same JSON Schema the MCP tool already declares. Host stays `orchestrate.js`. Plugin traps do not kill the orchestrator.

**Vs wasmtime-wit:** Extism = ship now. WIT = target ABI. Record both.

**2026-10-15 check:** license confirmed **BSD-3-Clause** (root `LICENSE`, crates.io metadata). Latest release **v1.41.0** (2026-10-09); the `extism` crate 1.41.0 declares `wasmtime ^49` / `wasmtime-wasi ^49`, so a host gets the 2026-10-14 security fixes (49.0.3) with `cargo update -p wasmtime`. Check the lockfile resolves >= 49.0.3 before shipping a plugin host (see **wasmtime-wit** for the advisory list).

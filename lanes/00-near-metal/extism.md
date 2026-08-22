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
    "https://extism.org/docs/overview"
  ],
  "license": "UNKNOWN (badge present, SPDX not opened)",
  "metal": 4,
  "determinism": 3,
  "revvel_hit": "mcp-product / control-plane tools as signed Wasm + XTP schema, not more Node",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22"
}
```

Live Wasm plugin host + PDKs (Rust/JS/Python/Go/Zig/…). XTP: schema → plugin bindgen. Host-gated HTTP. Not the full WASI Component Model.

Several 2026 hosts are moving Extism → native Wasmtime+WIT. Extism still wins when you need a PDK today.

**Revvel hit:** `OUTPUT_TYPE=mcp-product` as a signed `.wasm` with the same JSON Schema the MCP tool already declares. Host stays `orchestrate.js`. Plugin traps do not kill the orchestrator.

**Vs wasmtime-wit:** Extism = ship now. WIT = target ABI. Record both.

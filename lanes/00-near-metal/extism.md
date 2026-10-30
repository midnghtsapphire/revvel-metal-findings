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
  "updated": "2026-10-30"
}
```

Live Wasm plugin host + PDKs (Rust/JS/Python/Go/Zig/…). XTP: schema → plugin bindgen. Host-gated HTTP. Not the full WASI Component Model.

Several 2026 hosts are moving Extism → native Wasmtime+WIT. Extism still wins when you need a PDK today.

**Revvel hit:** `OUTPUT_TYPE=mcp-product` as a signed `.wasm` with the same JSON Schema the MCP tool already declares. Host stays `orchestrate.js`. Plugin traps do not kill the orchestrator.

**Vs wasmtime-wit:** Extism = ship now. WIT = target ABI. Record both.

**2026-10-15 check:** license confirmed **BSD-3-Clause** (root `LICENSE`, crates.io metadata). Latest release **v1.41.0** (2026-10-09); the `extism` crate 1.41.0 declares `wasmtime ^49` / `wasmtime-wasi ^49`, so a host gets the 2026-10-14 security fixes (49.0.3) with `cargo update -p wasmtime`. Check the lockfile resolves >= 49.0.3 before shipping a plugin host (see **wasmtime-wit** for the advisory list).

**2026-10-20 check:** no new Extism release (crates.io and GitHub still **1.41.0**). The Wasmtime floor rose to **>= 49.0.4** on 2026-10-19 (critical aarch64 Cranelift sandbox escape GHSA-mghf-wjfp-p5xm; see **wasmtime-wit**). `wasmtime ^49` still admits it, so a host picks it up with `cargo update -p wasmtime`; check the lockfile resolves **>= 49.0.4** (not 49.0.3) before shipping a plugin host. Verified via crates.io API and GitHub releases API, 2026-10-20 (America/Denver).

**2026-10-30 check:** no new Extism release (GitHub and crates.io still **1.41.0**). The Wasmtime floor rose to **>= 49.0.5** on the 49 line (2026-10-29: component resource-transfer memory bug GHSA-6fr9-xmw9-5352 and four others; see **wasmtime-wit**). `wasmtime ^49` admits 49.0.5, so `cargo update -p wasmtime`; check the lockfile resolves **>= 49.0.5** before shipping a plugin host. Verified via crates.io API and GitHub releases API, 2026-10-30 (America/Denver).

# Wasmtime + WIT Component Model

```json
{
  "id": "wasmtime-wit",
  "name": "Wasmtime Component Model / WIT",
  "lane": "00-near-metal",
  "status": "active",
  "urls": [
    "https://github.com/bytecodealliance/wasmtime",
    "https://component-model.bytecodealliance.org/",
    "https://docs.wasmtime.dev/examples-pulley.html"
  ],
  "license": "Apache-2.0 (Wasmtime)",
  "metal": 5,
  "determinism": 4,
  "revvel_hit": "engines/CONTRACT.md + a WIT world next to schemas/state.schema.json",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22",
  "updated": "2026-08-27"
}
```

Typed, sandboxed plugins. The contract is a WIT world, compile-checked, not a prompt. Hosts (Rust/Zig/C) load `.wasm` components; guests can be Rust, TinyGo, or other WIT-capable languages.

Extism is the easier PDK path (Go/JS/C). Several 2026 migrations (e.g. unicity-astrid) are moving Extism → native Wasmtime Component Model to drop ABI glue.

**Pulley (2026-08-27):** Wasmtime’s portable interpreter target (`pulley32` / `pulley64`). Cranelift AOT-compiles Wasm → Pulley bytecode for hosts Cranelift cannot natively JIT (or for portable embed). Expect ~10× slower than native; same API surface. Keeps the WIT world runnable on odd arches without a second ABI story.

**Revvel hit:** engines and runners should speak a WIT world. Orchestrator stays traffic-cop. A plugin trap must not kill the host. Pair with XGrammar so the coder emits WIT-valid interface stubs. Pulley is the fallback runtime, not a fork of the contract.

**Next trial:** one engine (research or coder helper) as a wasm32-wasip2 component with a 20-line WIT file. If it cannot load in wasmtime CLI (native or `--target pulley64`), drop or mark CANNOT.

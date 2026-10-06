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
    "https://docs.wasmtime.dev/examples-pulley.html",
    "https://github.com/bytecodealliance/wasmtime/releases/tag/v49.0.2",
    "https://wasi.dev/releases/wasi-p3"
  ],
  "license": "Apache-2.0 (Wasmtime)",
  "metal": 5,
  "determinism": 4,
  "revvel_hit": "engines/CONTRACT.md + a WIT world next to schemas/state.schema.json",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22",
  "updated": "2026-10-06"
}
```

Typed, sandboxed plugins. The contract is a WIT world, compile-checked, not a prompt. Hosts (Rust/Zig/C) load `.wasm` components; guests can be Rust, TinyGo, or other WIT-capable languages.

Extism is the easier PDK path (Go/JS/C). Several 2026 migrations (e.g. unicity-astrid) are moving Extism → native Wasmtime Component Model to drop ABI glue.

**Pulley (2026-08-27):** Wasmtime’s portable interpreter target (`pulley32` / `pulley64`). Cranelift AOT-compiles Wasm → Pulley bytecode for hosts Cranelift cannot natively JIT (or for portable embed). Expect ~10× slower than native; same API surface. Keeps the WIT world runnable on odd arches without a second ABI story.

**WASI 0.3 + security floor (2026-10-06):** Wasmtime 46 (2026-06-22) was the first release to implement final WASI 0.3.0 and turns on `component-model-async` by default (`async func`, `stream`, `future`; `wasi:io` is gone). WASI 0.3.1 shipped 2026-08-11 (`map<K,V>`, `implements`); 0.3.2 is planned for 2026-10-13. Latest Wasmtime is **v49.0.2** (2026-10-02), a security release that fixes, among others, an unvalidated async-lifted callback result count in the component model (native stack buffer overflow, GHSA-32h6-97mm-8q3c), a guest-triggered host panic via pre-epoch filesystem timestamps on wasip3 (GHSA-mr2v-56j5-cmfc), and WASI p0 `poll_oneoff` bypassing fuel (GHSA-j366-h8gg-77pm). Pin hosts to >= 49.0.2 before any plugin trial. Most guest toolchains still target WASI 0.2 (Rust has `wasip3` bindings; jco's 0.3 shim is experimental), and 0.3-capable Wasmtime still runs 0.2 components, so keep the trial on `wasm32-wasip2` and move to 0.3 async only when an engine needs streaming.

**Revvel hit:** engines and runners should speak a WIT world. Orchestrator stays traffic-cop. A plugin trap must not kill the host. Pair with XGrammar so the coder emits WIT-valid interface stubs. Pulley is the fallback runtime, not a fork of the contract.

**Next trial:** one engine (research or coder helper) as a wasm32-wasip2 component with a 20-line WIT file. If it cannot load in wasmtime CLI (native or `--target pulley64`), drop or mark CANNOT.

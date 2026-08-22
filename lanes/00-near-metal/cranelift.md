# Cranelift

```json
{
  "id": "cranelift",
  "name": "Cranelift",
  "lane": "00-near-metal",
  "status": "active",
  "urls": [
    "https://cranelift.dev/",
    "https://github.com/bytecodealliance/wasmtime/blob/main/cranelift/README.md"
  ],
  "license": "Apache-2.0 (in-tree with Wasmtime)",
  "metal": 5,
  "determinism": 4,
  "revvel_hit": "Pair with wasmtime-wit: engines compile to CLIF or wasm, not another Node runner",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Low-level retargetable code generator. Target-independent IR (CLIF) → executable machine code. Lives in the Wasmtime tree. Backends: x86-64, aarch64, s390x, riscv64. Production JIT/AOT for Wasmtime. Experimental Rust compiler backend. 2026 work includes `cranelift-codegen` `no_std` (merged Jan 2026, CI locked Mar 2026) so it can sit in a kernel or embed.

Fuzzed against V8 and the Wasm spec. Formal verification of instruction-selection backends is an active Bytecode Alliance effort. This is as close to the metal as this scrape goes without writing asm by hand.

**Revvel hit:** do not wrap another JS engine. If a runner must execute untrusted or generated code, Cranelift-under-Wasmtime is the compile step. WIT is the contract. Cranelift is the lowering.

**Next trial:** compile one tiny engine helper to wasm32-wasip2 and inspect `wasmtime compile` output. If we cannot name the Cranelift IR pass, we are still in essay land.

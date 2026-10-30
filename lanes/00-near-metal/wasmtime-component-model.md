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
    "https://github.com/bytecodealliance/wasmtime/releases/tag/v49.0.3",
    "https://github.com/bytecodealliance/wasmtime/security/advisories/GHSA-m9f7-9w4p-gv38",
    "https://wasi.dev/releases/wasi-p3",
    "https://github.com/WebAssembly/WASI/releases/tag/v0.3.2",
    "https://github.com/bytecodealliance/wasmtime/releases/tag/v49.0.4",
    "https://github.com/bytecodealliance/wasmtime/security/advisories/GHSA-mghf-wjfp-p5xm",
    "https://github.com/bytecodealliance/wasmtime/releases/tag/v50.0.0",
    "https://github.com/bytecodealliance/wasmtime/releases/tag/v50.0.1",
    "https://github.com/bytecodealliance/wasmtime/security/advisories/GHSA-6fr9-xmw9-5352",
    "https://github.com/bytecodealliance/wasmtime/security/advisories/GHSA-hmmr-87qq-258j"
  ],
  "license": "Apache-2.0 (Wasmtime)",
  "metal": 5,
  "determinism": 4,
  "revvel_hit": "engines/CONTRACT.md + a WIT world next to schemas/state.schema.json",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-08-22",
  "updated": "2026-10-30"
}
```

Typed, sandboxed plugins. The contract is a WIT world, compile-checked, not a prompt. Hosts (Rust/Zig/C) load `.wasm` components; guests can be Rust, TinyGo, or other WIT-capable languages.

Extism is the easier PDK path (Go/JS/C). Several 2026 migrations (e.g. unicity-astrid) are moving Extism → native Wasmtime Component Model to drop ABI glue.

**Pulley (2026-08-27):** Wasmtime’s portable interpreter target (`pulley32` / `pulley64`). Cranelift AOT-compiles Wasm → Pulley bytecode for hosts Cranelift cannot natively JIT (or for portable embed). Expect ~10× slower than native; same API surface. Keeps the WIT world runnable on odd arches without a second ABI story.

**WASI 0.3 + security floor (2026-10-06):** Wasmtime 46 (2026-06-22) was the first release to implement final WASI 0.3.0 and turns on `component-model-async` by default (`async func`, `stream`, `future`; `wasi:io` is gone). WASI 0.3.1 shipped 2026-08-11 (`map<K,V>`, `implements`); 0.3.2 is planned for 2026-10-13. Latest Wasmtime is **v49.0.2** (2026-10-02), a security release that fixes, among others, an unvalidated async-lifted callback result count in the component model (native stack buffer overflow, GHSA-32h6-97mm-8q3c), a guest-triggered host panic via pre-epoch filesystem timestamps on wasip3 (GHSA-mr2v-56j5-cmfc), and WASI p0 `poll_oneoff` bypassing fuel (GHSA-j366-h8gg-77pm). Pin hosts to >= 49.0.2 before any plugin trial (superseded 2026-10-15: >= 49.0.3). Most guest toolchains still target WASI 0.2 (Rust has `wasip3` bindings; jco's 0.3 shim is experimental), and 0.3-capable Wasmtime still runs 0.2 components, so keep the trial on `wasm32-wasip2` and move to 0.3 async only when an engine needs streaming.

**Security floor raised (2026-10-15):** Wasmtime **v49.0.3** (2026-10-14 11:17 MDT), **v48.0.6** (11:05 MDT) and **v36.0.18** (09:40 MDT) shipped with **15 advisories** published 2026-10-14 ~11:26 MDT. One **high**: filesystem sandbox escape when renaming symlinks with trailing slashes (GHSA-m9f7-9w4p-gv38; fixed in 36.0.18 / 48.0.6 / 49.0.3) -- this is the one that matters for any `--allow fs=` style grant. Two low: guests can send absolute-form HTTP requests to different hosts (GHSA-5qpp-g3j2-8frx, wasi-http host bypass) and unaligned host data from exception tags (GHSA-p79w-pv2r-29qp). The rest are medium, mostly guest-triggerable **host panics / DoS** in component-model async (cancelled `call_async`, yield in start function, async-lifted via `call`, pending calls after trap, stream/future type confusion, zero-length stream writes, overlapping string transcode in fused adapters -- 49.0.3 only), a stack overflow dropping long recursive-type chains, async-entrypoint not enforced, per-instance-only handle-table caps charged to no limit (GHSA-q554-3cjc-rx7p, also 36.0.18), and a wasi-http long-URL host crash. **New floor: pin hosts to >= 49.0.3 (or >= 48.0.6 / 36.0.18 LTS).** 49.0.2 is no longer enough. Wasmtime 50.0.0 is still `rc.1` on crates.io (final expected ~2026-10-20). WASI **0.3.2** released on the train 2026-10-13 07:23 MDT; its notes are governance/champion changes plus the 0.3.1 spec text, no new interfaces, so the trial target is unchanged.

**Revvel hit:** engines and runners should speak a WIT world. Orchestrator stays traffic-cop. A plugin trap must not kill the host. Pair with XGrammar so the coder emits WIT-valid interface stubs. Pulley is the fallback runtime, not a fork of the contract.

**Next trial:** one engine (research or coder helper) as a wasm32-wasip2 component with a 20-line WIT file. If it cannot load in wasmtime CLI (native or `--target pulley64`), drop or mark CANNOT.

**Security floor raised again (2026-10-20):** Wasmtime **v49.0.4** (published 2026-10-19 13:20 MDT), **v48.0.7** (13:20 MDT) and **v36.0.19** (13:09 MDT) fix five advisories published 13:20–13:21 MDT, plus a rustls bump to 0.23.46. One **critical**: on **aarch64**, Cranelift can compile a `br_table` with more than ~256k targets into a wrong conditional-branch target, letting a user-controlled module jump to arbitrary code -- a sandbox escape affecting every Wasmtime version with aarch64 support since 2020 (GHSA-mghf-wjfp-p5xm; fixed 36.0.19 / 48.0.7 / 49.0.4). **Medium:** wasi-http p3 guests can set an unchecked content-length on spliced response bodies (response splitting/injection, GHSA-9prg-84vf-g5fc; >= 46.0.0, fixed 48.0.7 / 49.0.4) and a host panic lowering a host-created component-model stream into a guest expecting a different payload type (GHSA-9pvw-hwfg-92h5). **Low:** wasi-http guests can add conflicting content lengths (GHSA-r8xh-cgf7-392j; also 36.0.19) and wasi-http p3 forwarded trailers skip the `is_forbidden_header` hook (GHSA-jxcf-8qw5-5c33). **New floor: pin hosts to >= 49.0.4 (or >= 48.0.7 / 36.0.19 LTS).** 49.0.3 is no longer enough; the aarch64 one matters for `ubuntu-24.04-arm` runners and Apple Silicon dev boxes. crates.io: max stable **49.0.4**, max version still `50.0.0-rc.1` (no 50.0.0 final yet). Trial target unchanged (`wasm32-wasip2`).

**Honesty (2026-10-20):** verified 2026-10-20 (America/Denver) via GitHub releases API (v49.0.4 / v48.0.7 bodies read; v36.0.19 listed), the repo security-advisories API for all five GHSA ids (severity, affected and patched ranges; critical advisory text read), release + advisory pages 200, crates.io API. Not run on the box.

**Wasmtime 50.0.0 final (2026-10-21):** **v50.0.0** published 2026-10-20 10:22 MDT (crates.io 10:16 MDT; Cranelift 0.137.0 alongside). crates.io max stable is now 50.0.0. Notable for revvel: the `wasmtime` CLI **no longer enables WASIp0 (`wasi_unstable`) by default** (`-Spreview0` to get it back); epoch-deadline and call-hook callbacks now get a `StoreHookState` instead of `StoreContextMut` (embedder API break); Winch no longer enables GC types, exceptions or tail calls by default; fuel is now saved/restored correctly around `call_ref` and exception catches; the `check-write` budget is enforced in `wasi:http` outgoing bodies; JIT code is made coherent with the instruction cache correctly on AArch64; `Engine::release_idle_pool_memory`; `wasmtime serve` can take systemd socket units and exit when idle. The 50.0.0 notes list no GHSA ids; 50.0.0 is outside the affected ranges of GHSA-mghf-wjfp-p5xm (affected `<36.0.19`, `>=37 <48.0.7`, `>=49 <49.0.4`). **Floor now: >= 50.0.0, or >= 49.0.4 / 48.0.7 / 36.0.19 on older lines.** Trial target unchanged (`wasm32-wasip2`); the WASIp0 default change does not touch it.

**Honesty (2026-10-21):** verified 2026-10-21 (America/Denver) via the GitHub releases API (v50.0.0 body read: Added / Changed / Fixed), the security-advisories API for GHSA-mghf-wjfp-p5xm (affected and patched ranges), and the crates.io API (`wasmtime` 50.0.0, `cranelift-codegen` 0.137.0). Not run on the box.

**Security floor raised (2026-10-30):** Wasmtime **v50.0.1**, **v49.0.5** and **v48.0.8** (2026-10-29), with **36.0.20** on crates.io, fix five advisories published 2026-10-29 ~13:06 MDT. **Medium:** wasi-sockets UDP could connect/send to an address that was only allowed for receiving (GHSA-hmmr-87qq-258j; `wasmtime-wasi`, 48-50); unchecked memory use when borrowed resources move between components (GHSA-6fr9-xmw9-5352; affected < 36.0.20, 37-48.0.7, 49.0.0-49.0.4, 50.0.0). **Low:** cross-engine type confusion (GHSA-qw58-7h65-crq2), a panic on i31/nullref typed functions (GHSA-3982-jqvv-277m), wasi-http p2 content-length (GHSA-h4wp-g4x3-7398). **New floor: >= 50.0.1, or >= 49.0.5 / 48.0.8 / 36.0.20.** 50.0.0 and 49.0.4 are no longer enough. The component-to-component one matters for any host that links more than one component; the socket one only if a helper gets a network grant. Trial target unchanged (`wasm32-wasip2`). Downstream: **wassette** v0.8.1 (48.0.6) and **act** 0.14.6 (49.0.2) are further below; **extism** 1.41.0 (`wasmtime ^49`) must lock >= 49.0.5.

**Honesty (2026-10-30):** verified 2026-10-30 (America/Denver) via the GitHub releases API (v50.0.1 / v49.0.5 / v48.0.8), the security-advisories API for all five GHSA ids (severity, affected and patched ranges), release and advisory pages 200, crates.io API (36.0.20 listed). Not run on the box.

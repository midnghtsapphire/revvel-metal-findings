# wassette

```json
{
  "id": "wassette",
  "name": "Wassette (microsoft/wassette)",
  "lane": "00-near-metal",
  "status": "active",
  "urls": [
    "https://github.com/microsoft/wassette",
    "https://github.com/microsoft/wassette/releases/tag/v0.8.0",
    "https://microsoft.github.io/wassette/v0.8.1/",
    "https://github.com/microsoft/wassette/releases/tag/v0.8.1",
    "https://github.com/microsoft/wassette/pull/895"
  ],
  "license": "MIT",
  "metal": 4,
  "determinism": 4,
  "revvel_hit": "wasmtime-wit trial host, but floor missed again: v0.8.1 (2026-10-18) pins Wasmtime 48.0.6, and the 2026-10-19 Wasmtime releases moved the floor to >= 48.0.7 / 49.0.4 (critical aarch64 sandbox escape + wasi-http fixes). Hold the trial until a wassette release pins >= 48.0.7 or >= 49.0.4. When unblocked: one coder/research helper (e.g. the WR schema checker) as a wasm32-wasip2 Component behind MCP with deny-by-default per-component storage/network/env grants; v0.8.1 refuses publisher-bundled OCI policies on automated/agent load paths and gives a component with no policy no env or secrets. Host stays orchestrate.js; not a second pipeline. Still self-described early development, so trial only",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12",
  "updated": "2026-10-30"
}
```

**Wassette** -- Microsoft's security-oriented runtime that serves WebAssembly Components as MCP tools. Built on Wasmtime; every component runs **deny-by-default** with its own permission set (storage paths, outbound network hosts, environment variables), enforced by the Wasm sandbox at runtime. Components load from OCI refs or local files; documented client setups for Claude Code, Codex CLI, GitHub Copilot / Copilot CLI. Components are generic WIT components, nothing MCP-specific inside them. **v0.8.0** (2026-09-29) adds an experimental `wassette acp` host (Agent Client Protocol over stdio, `wassette:acp@7.0.0` WIT package; layered chains share one WASI context, so grants are shared and chains with grants/secrets/`--allow-all` must opt in with `--allow-shared-grants`). v0.7.1 (2026-09-12) moved Wasmtime 47.0.3 → 47.0.4 for RUSTSEC-2026-0269 (filesystem sandbox escape) and one more advisory. MIT; ~964★; repo pushed 2026-10-06. README still says "Early Development: not production ready".

**Revvel hit:** the cheapest way to run the **wasmtime-wit** "one engine as a wasm32-wasip2 component" trial with an MCP front door the coder already speaks: a WIT world for the helper, explicit grants per component, a trap stays inside the sandbox. Same orchestrator, one sandboxed tool host; not a second pipeline. Pairs with **mcp-gate** (call policy) and **agentgate** (tool-surface lock).

**Honesty:** CAN-PARTIAL. Verified 2026-10-12 (America/Denver): repo, v0.8.0 release page, and docs site all 200; permissions doc read at tag v0.8.0. **Security floor not met:** v0.8.0's `Cargo.toml` pins `wasmtime = 47.0.4`; `main` is at 48.0.3. Neither includes the 2026-10-02 Wasmtime security fixes (shipped in 49.0.2, 48.0.5, 36.0.17), and the 47.x line got no 2026-10-02 patch. Do not run it as the trial host until a release pins Wasmtime >= 48.0.5 or >= 49.0.2; watching until then. Also explicitly pre-production.

**Floor moved again (2026-10-15):** Wasmtime 49.0.3 / 48.0.6 / 36.0.18 (2026-10-14) fix 15 more advisories, including a high filesystem sandbox escape (GHSA-m9f7-9w4p-gv38). Wassette latest release still **v0.8.0**; `main` `Cargo.toml` (tip `d4911e49b8`, 2026-10-14 06:12 MDT) still pins `wasmtime` / `wasmtime-wasi` / `wasmtime-wasi-http` / `wasmtime-wasi-config` **48.0.3**. The recent pushes are dependabot bumps (tokio, tokio-util, rmcp 3.5.1, hyper, proptest), none to Wasmtime. Needs >= 48.0.6 or >= 49.0.3 now. Still watching.

**Update 2026-10-19 -- floor met, promoted to active:** **v0.8.1** released 2026-10-18 22:45 MDT (immutable release, tag commit `4ccdba57168068bdeb7f046fe24e85d5ee252125`). `Cargo.toml` at tag `v0.8.1` pins `wasmtime` / `wasmtime-wasi` / `wasmtime-wasi-http` / `wasmtime-wasi-config` **48.0.6**, and `Cargo.lock` resolves `wasmtime` 48.0.6, so it now sits on a patched line (the 2026-10-14 advisories, including the high fs sandbox escape GHSA-m9f7-9w4p-gv38, are fixed in 48.0.6). Release notes, security section: OCI artifacts that carry a **publisher-supplied policy are rejected by default**; a direct operator can activate one after review with `wassette component load <OCI-URI> --trust-bundled-policy`, while automated and agent-facing load paths stay fail closed (#888); components **without an attached policy no longer receive configured environment values or stored secrets** (#889); a rejected OCI policy load keeps the previously installed component, policy, metadata, and precompiled cache. Maintenance: Wasmtime, quinn-proto, rustls moved to patched releases. Repo ~967★, MIT, pushed 2026-10-18 23:08 MDT.

Status change: **watching → active**, ranked just ahead of **act** (act's 0.14.6 still locks Wasmtime 49.0.2, below the floor). Wassette is now the one Wasm-Component-over-MCP host on a patched Wasmtime release, and the v0.8.1 defaults (no ambient env, no self-granted bundled policy) are what a deliver:* helper host should do. Insertion is unchanged: one helper behind MCP, grants written by the operator, orchestrate.js stays the only orchestrator.

**Dead link fixed:** `https://microsoft.github.io/wassette/latest/` returns **404** this run (the README at v0.8.1 still links `/latest/…`); replaced with the versioned docs `https://microsoft.github.io/wassette/v0.8.1/` (200). The docs root `https://microsoft.github.io/wassette/` is also 200.

**Honesty (2026-10-19):** CAN-PARTIAL. Verified 2026-10-19 (America/Denver) via the GitHub releases API (v0.8.1 body read), raw `Cargo.toml` + `Cargo.lock` at tag `v0.8.1`, repo API (MIT, not archived), release page 200, versioned docs 200. README at v0.8.1 still says "Early Development: This repository is not production ready yet." Not run on the box. The ACP layered-chain shared-grant caveat from v0.8.0 still applies if `wassette acp` is used; the MCP path is what the trial needs.

**Update 2026-10-20 -- floor missed again:** Wasmtime **48.0.7 / 49.0.4** shipped 2026-10-19 ~13:20 MDT with one critical advisory (aarch64 Cranelift `br_table` miscompile → sandbox escape, GHSA-mghf-wjfp-p5xm) and four wasi-http / component-model ones (see **wasmtime-wit**). Wassette's latest release is still **v0.8.1** on **48.0.6**, so it is below the new floor. `main` (tip `81dcf122b6`, 2026-10-19 19:14 MDT) still pins `wasmtime` / `wasmtime-wasi` / `wasmtime-wasi-http` / `wasmtime-wasi-config` **48.0.6**; the latest pushes are dependabot bumps (sha2, serde_json, wasmparser). Dependabot **PR #895** (opened 2026-10-19 19:13 MDT, open) bumps the wasmtime group 48.0.6 → **49.0.3**, which is itself below the new 49.0.4 floor (it replaced #800, closed the same minute). Status stays **active** (same convention as **act**: right design, one Wasmtime patch away), rank unchanged, but **do not run the trial on v0.8.1**: wait for a release pinning >= 48.0.7 / 49.0.4, or build from source after `cargo update -p wasmtime --precise 48.0.7` (and the wasi crates). The critical issue is aarch64-only; the wasi-http ones matter only if the helper gets a network grant.

**Honesty (2026-10-20):** verified 2026-10-20 (America/Denver): GitHub releases API (latest still v0.8.1), raw `Cargo.toml` on `main`, commits API, PR #895 page 200 and body read (48.0.6 → 49.0.3). Not run on the box.

**Update 2026-10-30 -- floor moved again:** Wasmtime 50.0.1 / 49.0.5 / 48.0.8 (2026-10-29) fix five more advisories (see **wasmtime-wit**), so the floor is now **>= 48.0.8 / 49.0.5 / 50.0.1**. Wassette's latest release is still **v0.8.1** (Wasmtime 48.0.6), two patches behind on its line. Trial stays on hold: wait for a release pinning >= 48.0.8 / 49.0.5, or build from source after `cargo update -p wasmtime --precise 48.0.8` (and the wasi crates). Verified 2026-10-30 (America/Denver) via GitHub releases API. `main` not re-read.

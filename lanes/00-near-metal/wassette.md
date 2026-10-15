# wassette

```json
{
  "id": "wassette",
  "name": "Wassette (microsoft/wassette)",
  "lane": "00-near-metal",
  "status": "watching",
  "urls": [
    "https://github.com/microsoft/wassette",
    "https://github.com/microsoft/wassette/releases/tag/v0.8.0",
    "https://microsoft.github.io/wassette/latest/"
  ],
  "license": "MIT",
  "metal": 4,
  "determinism": 4,
  "revvel_hit": "wasmtime-wit trial host: run coder/research helper tools as wasm32-wasip2 Components behind MCP with deny-by-default per-component storage/network/env grants, instead of hand-rolling a Wasmtime host; blocked until a release ships Wasmtime on a patched line (>= 49.0.3 / 48.0.6 as of 2026-10-15)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-12",
  "updated": "2026-10-15"
}
```

**Wassette** -- Microsoft's security-oriented runtime that serves WebAssembly Components as MCP tools. Built on Wasmtime; every component runs **deny-by-default** with its own permission set (storage paths, outbound network hosts, environment variables), enforced by the Wasm sandbox at runtime. Components load from OCI refs or local files; documented client setups for Claude Code, Codex CLI, GitHub Copilot / Copilot CLI. Components are generic WIT components, nothing MCP-specific inside them. **v0.8.0** (2026-09-29) adds an experimental `wassette acp` host (Agent Client Protocol over stdio, `wassette:acp@7.0.0` WIT package; layered chains share one WASI context, so grants are shared and chains with grants/secrets/`--allow-all` must opt in with `--allow-shared-grants`). v0.7.1 (2026-09-12) moved Wasmtime 47.0.3 → 47.0.4 for RUSTSEC-2026-0269 (filesystem sandbox escape) and one more advisory. MIT; ~964★; repo pushed 2026-10-06. README still says "Early Development: not production ready".

**Revvel hit:** the cheapest way to run the **wasmtime-wit** "one engine as a wasm32-wasip2 component" trial with an MCP front door the coder already speaks: a WIT world for the helper, explicit grants per component, a trap stays inside the sandbox. Same orchestrator, one sandboxed tool host; not a second pipeline. Pairs with **mcp-gate** (call policy) and **agentgate** (tool-surface lock).

**Honesty:** CAN-PARTIAL. Verified 2026-10-12 (America/Denver): repo, v0.8.0 release page, and docs site all 200; permissions doc read at tag v0.8.0. **Security floor not met:** v0.8.0's `Cargo.toml` pins `wasmtime = 47.0.4`; `main` is at 48.0.3. Neither includes the 2026-10-02 Wasmtime security fixes (shipped in 49.0.2, 48.0.5, 36.0.17), and the 47.x line got no 2026-10-02 patch. Do not run it as the trial host until a release pins Wasmtime >= 48.0.5 or >= 49.0.2; watching until then. Also explicitly pre-production.

**Floor moved again (2026-10-15):** Wasmtime 49.0.3 / 48.0.6 / 36.0.18 (2026-10-14) fix 15 more advisories, including a high filesystem sandbox escape (GHSA-m9f7-9w4p-gv38). Wassette latest release still **v0.8.0**; `main` `Cargo.toml` (tip `d4911e49b8`, 2026-10-14 06:12 MDT) still pins `wasmtime` / `wasmtime-wasi` / `wasmtime-wasi-http` / `wasmtime-wasi-config` **48.0.3**. The recent pushes are dependabot bumps (tokio, tokio-util, rmcp 3.5.1, hyper, proptest), none to Wasmtime. Needs >= 48.0.6 or >= 49.0.3 now. Still watching.

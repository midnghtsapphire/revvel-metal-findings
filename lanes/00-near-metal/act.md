# act (ACT — Agent Component Tools)

```json
{
  "id": "act",
  "name": "ACT — Agent Component Tools (actcore/act-cli)",
  "lane": "00-near-metal",
  "status": "active",
  "urls": [
    "https://github.com/actcore/act-cli",
    "https://github.com/actcore/act-cli/releases/tag/0.14.6",
    "https://www.npmjs.com/package/@actcore/act",
    "https://actcore.dev/docs/",
    "https://actcore.dev/blog/2026-10-05-sandboxed-agent-tools/"
  ],
  "license": "MIT OR Apache-2.0",
  "metal": 4,
  "determinism": 4,
  "revvel_hit": "wasmtime-wit trial host (one Wasmtime patch behind the floor as of 2026-10-15): run a coder/research helper as a wasm32-wasip2 Component served over MCP stdio (`act run --mcp`) with undeclared = denied, declared = waits for an explicit `--allow`, headless = deny, and an always-on audit trail; Cargo.lock still Wasmtime 49.0.2, below the new >= 49.0.3 floor (2026-10-14 advisories incl. high fs sandbox escape); wait for a re-pinned release or rebuild with `cargo update -p wasmtime` before the trial. Still closer than wassette. Host stays orchestrate.js; not a second pipeline",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-13",
  "updated": "2026-10-30"
}
```

**ACT** (Agent Component Tools) -- packages an agent tool as one WebAssembly Component that **declares** what it needs (filesystem globs, HTTP hosts, sockets, credentials); the Rust + Wasmtime host enforces it. Anything undeclared is denied; anything declared still waits for an operator grant (`--allow 'fs=/data/**'`, `--allow 'http=https://api.example.com'`, `--deny` to carve back out, or a `[policy]` section in `~/.config/act/config.toml`). Default mode is ask; a **headless call with no grant degrades to deny**. `act info` shows what a component can touch before it runs. The same `.wasm` serves MCP over stdio (`act run --mcp`) or Streamable HTTP, runs as a CLI (`act call`), or runs in a browser tab. Components load from OCI refs (optional `@sha256:` digest), HTTP URLs, or local files; components published to actpkg.dev are signed with keyless cosign in CI (per the 2026-10-05 blog post). Audit trail on stderr is on by default and does not follow `RUST_LOG`: component digest, resolved capability modes, every allow/deny/ask decision, per-call rollup with a SHA-256 digest of tool arguments; only `--no-audit` turns it off. SECURITY.md: OIDC trusted publishing to crates.io/PyPI/npm, Sigstore build provenance, CycloneDX SBOM per release.

Current release **0.14.6** (GitHub release 2026-10-07 16:01 MDT; tag `0.14.6` → `b591fe9e647ba8abe49ab3efa6846b0bf50d1477`; npm `@actcore/act` 0.14.6 published 2026-10-07 15:52 MDT; PyPI `act-cli` and crates.io `act-cli` also 0.14.6). `Cargo.lock` at tag 0.14.6 and on `main`: **`wasmtime` 49.0.2**. 0.14.4 (2026-10-03 06:48 MDT) moved Wasmtime 49.0.0 → 49.0.2, closing RUSTSEC-2026-0313…0316 and 0320…0327, including the async-lifted callback stack overflow (GHSA-32h6-97mm-8q3c, critical); 0.14.3 (2026-09-25) fixed host-rule bypass by respelling hosts (`127.1`, `0x7f.0.0.1`, trailing dot). Dual MIT OR Apache-2.0 (`Cargo.toml`, `LICENSE-MIT` + `LICENSE-APACHE`; GitHub's detector shows Apache-2.0). Repo created 2026-03-12, pushed 2026-10-10, ~2★, org-owned (`actcore`).

**Revvel hit:** the **wasmtime-wit** trial ("one engine as a wasm32-wasip2 component") needs a host that is on a patched Wasmtime line; **wassette** is still on 48.0.3 (main) / 47.0.4 (v0.8.0). ACT already ships 49.0.2, speaks MCP to the coder, and makes the grant explicit per call. Build one helper (e.g. the WR schema checker) as a component, run it with `act run --mcp <file.wasm> --allow <one dir>`, and keep orchestrate.js as the only orchestrator. Pairs with **mcp-gate** (call policy) and **agentgate** (tool-surface lock). Same pipeline, one sandboxed tool host.

**Floor moved (2026-10-15):** Wasmtime 49.0.3 / 48.0.6 / 36.0.18 shipped 2026-10-14 with 15 advisories, including a **high** filesystem sandbox escape when renaming symlinks with trailing slashes (GHSA-m9f7-9w4p-gv38) and a low wasi-http absolute-form request host bypass (GHSA-5qpp-g3j2-8frx) -- both relevant to ACT's `fs=` / `http=` grants. ACT's latest release is still **0.14.6** (PyPI/npm unchanged), and `Cargo.lock` on both tag `0.14.6` and `main` still resolves **`wasmtime` 49.0.2**. Last commit on `main` is the 0.14.6 release (2026-10-07); open PRs are dependabot (wasmparser, hclient), none for Wasmtime. Status stays active (one patch bump away, same 49.x line), but **do not run the trial on 0.14.6**: wait for an ACT release with Wasmtime >= 49.0.3, or build from source after `cargo update -p wasmtime --precise 49.0.3`.

**Honesty:** CAN-PARTIAL. Verified 2026-10-13 (America/Denver): repo live (not archived), release page 0.14.6 200, npm registry JSON 0.14.6 (npmjs.com web page 403s the fetcher, as for other npm entries), PyPI 0.14.6, crates.io API 0.14.6, docs site + blog 200, `Cargo.lock` read at tag. Young and tiny (~2★, single org); fast release cadence (0.14.2–0.14.6 in two weeks) -- pin an exact version and re-check the Wasmtime pin on each bump. A native MCP server must be rebuilt as a component to get the sandbox. Isolation is Wasm + capability policy, not a VM. Capability claims are from the README/SECURITY.md; not run on the box this scrape.

**Update 2026-10-19:** no new ACT release: GitHub releases latest still **0.14.6**; PyPI `act-cli` and npm `@actcore/act` still 0.14.6; `Cargo.lock` on `main` still resolves **`wasmtime` 49.0.2** (below the >= 49.0.3 floor); last commit on `main` is still the 0.14.6 release (2026-10-07). Open PRs are dependabot only (hclient-rt-tokio, hclient-dns, wasmparser, bytesize, oci-spec), none for Wasmtime. Meanwhile **wassette v0.8.1** (2026-10-18) shipped Wasmtime 48.0.6, so wassette moves ahead of ACT in INDEX as the trial host that meets the floor today. ACT stays active (its grant model and audit trail are still the better fit once re-pinned); do not trial 0.14.6 as shipped. Verified 2026-10-19 (America/Denver) via GitHub releases/commits/pulls API, raw `Cargo.lock` on `main`, PyPI + npm registry JSON.

**Update 2026-10-20:** still no ACT release (GitHub, PyPI `act-cli`, npm `@actcore/act`, crates.io all **0.14.6**); `Cargo.lock` on `main` still resolves **`wasmtime` 49.0.2**. The floor moved again on 2026-10-19 to **>= 49.0.4** (Wasmtime 49.0.4 / 48.0.7: critical aarch64 Cranelift sandbox escape GHSA-mghf-wjfp-p5xm plus wasi-http fixes; see **wasmtime-wit**), so ACT is now two patch releases behind. No Wasmtime PR open (latest Wasmtime bump PR in the repo is from 2026-08). Status unchanged: active, do not trial 0.14.6; re-pin with `cargo update -p wasmtime --precise 49.0.4` or wait for a release. Verified 2026-10-20 (America/Denver) via registry JSON (PyPI, npm, crates.io API), GitHub releases API, raw `Cargo.lock` on `main`, PR search.

**Update 2026-10-30:** still no ACT release (crates.io `act-cli` **0.14.6**). The Wasmtime floor rose again on 2026-10-29 to **>= 49.0.5** on the 49 line (five advisories; see **wasmtime-wit**), so ACT's 49.0.2 lock is now three patch releases behind. Status unchanged: active, do not trial 0.14.6; re-pin with `cargo update -p wasmtime --precise 49.0.5` or wait for a release. Verified 2026-10-30 (America/Denver) via crates.io API. `Cargo.lock` on `main` not re-read.

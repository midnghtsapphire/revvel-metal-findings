# agent-spec

```json
{
  "id": "agent-spec",
  "name": "agent-spec",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/ZhangHanDong/agent-spec",
    "https://lib.rs/crates/agent-spec",
    "https://docs.rs/agent-spec"
  ],
  "license": "MIT",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "wr:code / spec-approved / deliver:* — intent→Requirement IR→Task Contracts→lifecycle/guard mechanical verify; CLI+MCP beside existing orchestrate.js, no second spine",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-28"
}
```

**agent-spec** -- Rust **intent compiler** for AI coding. Human intent compiles through structured Requirement IR (`REQ-*`) into verifiable Task Contracts (`specs/*.spec.md` with Intent / Decisions / Boundaries / Completion Criteria + explicit test selectors); agents implement against the contract; the machine verifies via `lifecycle` / `guard` / `trace` (lint → structural → boundaries → bound tests). Dual-IR: Requirement IR (governed truth) + Code Graph IR (Rust Atlas, rebuildable). Gates between intake and acceptance are **deterministic and model-free**; AI only at the edges (draft candidates, implement). MCP server (read-only knowledge/specs). crates.io **`agent-spec==1.4.0`** (2026-08-17 "enforcement" release); MIT; ~457★; created 2026-03-07; last push noted 2026-09-23. 1.0 compatibility promise on CLI + machine formats + governance semantics.

**Revvel hit:** closest live metal for making `research:complete` → `spec-approved` → `wr:code` → `deliver:*` a **compile-then-verify** chain instead of an essay. Map Task Contracts onto WR / `standards/shapes`; run `agent-spec lifecycle` / `guard` in CI next to **agentverify** cassettes; keep human Approve/Authorize on **spec-guard**. Pair with **contract-agent** (runtime CEL refuse) and **compiled-ai** (LLM out of control plane after compile). Do **not** stand up a parallel orchestrator — CLI tool + MCP beside `orchestrate.js`.

**Honesty:** CAN-PARTIAL. Verified 2026-09-28 (America/Denver): GitHub `ZhangHanDong/agent-spec` live (457★, MIT LICENSE, Rust 2024); lib.rs / docs.rs show **1.4.0**; release notes + Cargo.toml `version = "1.4.0"`. Pattern + CLI, not a drop-in for `orchestrate.js`. Rust-atlas-first for code graph; Node/TS WR path still needs explicit test bindings you own. Approval identity stays outside the compiler (ADR-001) — bind to existing human gates.

# hlv

```json
{
  "id": "hlv",
  "name": "hlv",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/lee-to/hlv",
    "https://hlv.cutcode.dev/",
    "https://github.com/lee-to/hlv/releases/tag/v1.0.1"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Watch: Rust proof binary (hlv check / gates / MCP) for contract→code traceability — prefer agent-spec lifecycle for wr:code; hlv is fuller SDD harness (llm/ ownership risk)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-28"
}
```

**hlv** -- compiled Rust binary for Spec-Driven Development with LLMs. Three hard layers: human owns WHAT (artifacts, constraints, milestones), LLM owns HOW (all code under `llm/`), **hlv validates PROOF** (`hlv check` — 30+ validations across contracts, traceability, gates, constraints; does not call the LLM). MCP server (stdio/SSE). `hlv init --adopt` for existing codebases. Site: https://hlv.cutcode.dev/. **v1.0.1** released 2026-09-20; MIT; ~80★; created 2026-03-09.

**Revvel hit:** useful as a **watching** proof-binary pattern next to **agent-spec** / **spec-guard**, but the greenfield doc stance ("entire `llm/` layer owned by the LLM") is a second-pipeline trap for revvel-standards. Prefer **agent-spec** `lifecycle`/`guard` as the mechanical verify CLI that plugs into existing WR files; keep **spec-guard** for hash-bound human Approve/Authorize. Revisit if adopt-mode maps cleanly onto `engines/` + `schemas/` without relocating craft out of `scripts/`.

**Honesty:** CAN-PARTIAL. Verified 2026-09-28 (America/Denver): GitHub `lee-to/hlv` live (80★, MIT LICENSE, Cargo.toml `1.0.1`); release tag `v1.0.1` 200; site 200. Watching — not default wire — because full harness ownership conflicts with "no second pipeline."

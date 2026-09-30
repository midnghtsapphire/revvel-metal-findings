# GovernSpec

```json
{
  "id": "governspec",
  "name": "GovernSpec",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/SymbolicLight-AGI/GovernSpec",
    "https://pypi.org/project/governspec/"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "wr:code / spec-approved / deliver:* — one govern.yaml → AGENTS.md / Cursor rules / OpenAI structured-output schemas / MCP plan + offline acceptance tests; compile beside existing handoff, no second spine",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-30"
}
```

**GovernSpec** -- local-first **YAML task-contract compiler** for AI agent workflows. One `govern.yaml` (goals, permissions, constraints, human approval gates, output format/schema, acceptance tests) validates → resolves GovernPack imports → normalizes to IIR → compiles to tool artifacts (`agents-md`, `claude-md`, `cursor-rules`, `openai-structured`, `gemini-structured`, `mcp-plan`, `skill`, …) and runs **deterministic offline** `governspec test` assertions (`required_sections`, `json_schema`, `regex`, `max_words`, …). Explicitly **not** an LLM runtime, orchestrator, permission sandbox, or runtime enforcer — express/distribute/check only. Thin MCP server (`governspec.validate|inspect|compile|test`). Python ≥3.11; **PyPI `governspec==0.1.0`** (2026-05-12); MIT LICENSE + CITATION.cff 0.1.0; ~2★; tip `cfc54c1aac0dce1c638d2ede80c4ddf8bbdd0197` (Codex plugin preview). Alpha (PyPI Development Status 3).

**Revvel hit:** map `govern.yaml` onto WR shapes so `research:complete` → `spec-approved` emits the same structured-output / Cursor / MCP artifacts the cage already consumes, then gate `deliver:*` dumps with offline `governspec test`. Pair with **spec-guard** (hash-bound human Approve/Authorize — GovernSpec only *declares* `human_gates`), **contract-agent** (CEL refuse at tool time), **agent-spec** (REQ IR → Task Contracts), **compiled-ai** (LLM out of control plane after compile). Prefer MIT over AGPL alternatives for the proprietary spine. Do **not** stand up a parallel agent runtime.

**Honesty:** CAN-PARTIAL. Verified 2026-09-30 (America/Denver): GitHub `SymbolicLight-AGI/GovernSpec` 200 (MIT LICENSE, packages/{governspec-core,cli,mcp,ts,vscode}, examples/, schema/, tests/); PyPI `governspec` 0.1.0 200. Compile + assert offline only — **no** runtime tool/mask enforcement (author-stated). Young (2★, last push 2026-05-12). Not a drop-in for `orchestrate.js`.

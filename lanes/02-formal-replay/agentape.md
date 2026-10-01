# agentape

```json
{
  "id": "agentape",
  "name": "agentape",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/matsurih/agentape",
    "https://www.npmjs.com/package/agentape"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "deliver:* CI — process-boundary record/replay of HTTP + MCP tool/JSON-RPC cassettes wrapping existing test command; no second orchestrator",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-01"
}
```

**agentape** -- VCR / nock pattern for AI agents at the **process boundary**: `agentape record <cmd>` / `agentape replay <cmd>` wraps an existing test command (no SDK monkey-patch). Captures HTTP, MCP tool calls, and MCP JSON-RPC into plain JSON cassettes; replay serves stored responses with **deterministic matching** and fail-closed unmatched calls (non-zero exit + closest-match diffs). Includes `agentape mcp-proxy` for MCP client configs. TypeScript; **npm `agentape@0.1.0`** (MIT; published 2026-04-28); ~3★; tip `362de8b33d5a95415390b402ac9374d80088c24d`.

**Revvel hit:** wrap `deliver:*` / label-graph integration tests that hit live MCP or HTTP so CI replays without tokens or external APIs — complements **agentverify** (pytest YAML cassettes / tool-sequence asserts) and **chronos-dst** / **unflake** (Node DST). Prefer when the host has no library hook surface. Do **not** invent a parallel agent OS.

**Honesty:** CAN-PARTIAL. Verified 2026-10-01 (America/Denver): GitHub `matsurih/agentape` 200 (MIT LICENSE); npm `agentape` 0.1.0 200. Early 0.1.0; last push 2026-04-28. Process-boundary only — does not replace in-process assertions from **agentverify**.

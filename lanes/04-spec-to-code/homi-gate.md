# homi-gate

```json
{
  "id": "homi-gate",
  "name": "homi-gate",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/homayoun-safarpour/homi-gate"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "deliver:* / wr:code — fail-closed CI on completion bit, handoff contracts (from/to/proved/pending/stop), and MCP allowlist shape; no LLM judge",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-02"
}
```

**homi-gate** -- thin fail-closed CLI for agent pipeline CI: three deterministic checks, exit `0`/`1`, no model in the loop. (1) **completion bit** — truncated/incomplete receipts fail; (2) **handoff contract** — null `context`, missing `stop`/`proved`/… fail; (3) **MCP allowlist** — open “enable whole server” shapes fail (needs allowlist+denylist or `enabled: false` with named tools). Python ≥3.11; PyYAML; `homi-gate` console script; MIT; tip `5df6fcf643ffe698f77052e89f8b6e50bca5cf89`; v0.1.0 alpha; 0★; created 2026-09-30. Not on PyPI yet (install from source).

**Revvel hit:** wire `check-completion` / `check-handoff` / `check-mcp-allowlist` beside existing `deliver:*` CI so truncated WR dumps, null handoffs, and open MCP configs cannot go green — not a second orchestrator. Pair with **spec-guard** (hash-bound human Approve/Authorize), **aicontracts** (YAML effects + check-verdict), **agent-gate** (runtime ship checklist + receipts).

**Honesty:** CAN-PARTIAL. Verified 2026-10-02 (America/Denver): GitHub live, MIT LICENSE, pyproject 0.1.0. Young hire-signal OSS (0★); schema dialects may need alias mapping to Revvel receipt shapes. Not a grammar mask engine.

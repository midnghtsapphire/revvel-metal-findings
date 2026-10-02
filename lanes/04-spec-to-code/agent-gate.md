# agent-gate

```json
{
  "id": "agent-gate",
  "name": "agent-gate (mcp-agent-gate)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/Jott2121/agent-gate",
    "https://pypi.org/project/mcp-agent-gate/"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "deliver:* — MCP fail-closed ship checklist + sha256 hash-chained receipts before agent claims done; human_gated_if_irreversible required",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-02"
}
```

**agent-gate** (PyPI `mcp-agent-gate`) -- MCP server that gates an agent's claim of “done”: fail-closed checklist (`verify_gate`) then append-only **sha256 hash-chained** receipts ledger (`record_receipt` / `read_receipts`). Default `ship` gate: `deterministic_checks_pass`, `independent_refute_review`, `no_secrets`, `human_gated_if_irreversible`, `honest_receipt_logged`. Stdlib core (`gate.py`, `ledger.py`) + thin MCP adapter. MIT; PyPI **0.1.1**; tip `ef91c37ed7d1fff42478bc8020c35fd06a163caa` (mcp 2.x FastMCP→MCPServer compat); ~3★.

**Revvel hit:** call `verify_gate` before the `deliver:*` coder stamps complete; store receipts next to the WR close — complements **spec-guard** (human Approve/Authorize on work packets) and **homi-gate** (CI on handoff JSON). Prefer MIT over AGPL **agentassert-abc**.

**Honesty:** CAN-PARTIAL. Verified 2026-10-02 (America/Denver): GitHub + MIT LICENSE + PyPI 0.1.1 live. Evidence dict is agent-supplied (fail-closed on missing keys, not on forged true). Not a tool-call policy enforcer (see **verax** / **contract-agent**).

# AgentAssert (ABC)

```json
{
  "id": "agentassert-abc",
  "name": "AgentAssert (ABC)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/qualixar/agentassert-abc",
    "https://pypi.org/project/agentassert-abc/",
    "https://arxiv.org/abs/2602.22302"
  ],
  "license": "AGPL-3.0",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "deliver:* tool refuse — MCP guard wraps tools/call under YAML behavioral contracts; prefer MIT contract-agent/spec-guard unless commercial license clears AGPL",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-30"
}
```

**AgentAssert** -- formal **Agent Behavioral Contracts (ABC)** with runtime enforcement. YAML ContractSpec DSL (14 operators; hard/soft constraints + recovery) → adapters (LangGraph, CrewAI, OpenAI Agents, …) and an **`agentassert-abc-mcp-guard`** that wraps any MCP server and screens `tools/call` both ways. Adds session drift (JSD), (p,δ,k)-satisfaction, SPRT certification, compositional pipeline bounds (paper arXiv:2602.22302). AgentContract-Bench: 293 scenarios / 12 domains. Python ≥3.12; **PyPI `agentassert-abc==0.7.1`**; ~6★; dual-license **AGPL-3.0-or-later** + commercial.

**Revvel hit:** MCP guard is the interesting metal for refusing illegal `deliver:*` tool calls without rewriting the host — but **AGPL-3.0** is a hard adoptability flag for proprietary `revvel-standards`. Prefer **contract-agent** (MIT CEL) + **spec-guard** (MIT hash gates) on the spine; keep AgentAssert watching until a commercial license or a MIT-compatible subset is in play. Do not invent a second orchestrator.

**Honesty:** CAN-PARTIAL. Verified 2026-09-30 (America/Denver): GitHub `qualixar/agentassert-abc` 200 (AGPL LICENSE); PyPI 0.7.1 200; arXiv 2602.22302 200. Last substantive tip commits August 2026 (docs/badge refresh). Enforcement covers MCP tools / framework hooks — not built-in editor/shell. AGPL copyleft + commercial track required for closed products.

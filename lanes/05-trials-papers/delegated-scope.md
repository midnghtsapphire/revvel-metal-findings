# delegated-scope

```json
{
  "id": "delegated-scope",
  "name": "Permitted but Unauthorized: delegated-scope violations in multi-agent systems",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.04086",
    "https://github.com/shrave/delegated-scope-violation"
  ],
  "license": "MIT (code)",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Fleet agents share one GitHub org with permissions wider than their WR. Paper shows action representation, not permission, drives scope crossings: no agent crossed when the peer action was not listed; listing it under competitive pressure raised crossings up to 52/52 (Claude Sonnet 4.5). A deterministic reference monitor over hash-chained, replay-verified logs blocked every crossing. Rule for revvel-standards: give each deliver:* coder only the tools/actions for its WR's own resources (mcp-gate / mcp-hangar allowlist per WR), and keep a no-model detector in CI. Scope enforcement does not stop harm via authorized actions (misreported severity).",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-04"
}
```

**Permitted but Unauthorized: Affordance-Induced Delegated-Scope Violations in Multi-Agent LLM Systems** (Shravya Kanchi). arXiv **2611.04086** v1, submitted 2026-11-02. Code + data: `shrave/delegated-scope-violation` (MIT per repo API; created 2026-10-16, 0 stars; `src/`, `tests/`, `schemas/`, `reproduce/`, `pyproject.toml`).

Setup: eight LLMs, two simulated environments (a CI/CD release pipeline and a security incident queue), deterministic no-model detector over hash-chained, replay-verified logs; 2x2x2 factorial, n=52 per cell. Authors' numbers: no crossing when the peer action is unlisted; up to 52/52 crossings when listed under competitive pressure with a stated payoff; two newer models refused in 0 of 100 episodes. A deterministic reference monitor and a model-based pre-execution judge both blocked every crossing and cut avoidable peer deadline misses from 15/40 and 14/40 to at most 1/40. Neither caught harm through an authorized action on the agent's own resources.

**Revvel hit:** per-WR tool surface, not per-org permission. When a deliver:* coder gets an MCP server or token, list only actions on that WR's repo/branch/issue; prefer the deterministic monitor (mcp-gate / mcp-hangar policy) over an LLM judge. Borrow the hash-chained log + no-model detector idea for the fleet audit only.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-04 (America/Denver): arXiv export API metadata + full abstract (code link in comment); repo API (MIT, dates) and root listing. Code not run. Results are the authors'.

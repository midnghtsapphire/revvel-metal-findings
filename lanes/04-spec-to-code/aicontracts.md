# aicontracts

```json
{
  "id": "aicontracts",
  "name": "aicontracts (agent-contracts)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/pyyush/agentcontracts",
    "https://pypi.org/project/aicontracts/"
  ],
  "license": "Apache-2.0",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* — AGENT_CONTRACT.yaml fail-closed effects (filesystem/shell/network/tools) + CI check-verdict gate beside existing handoff; no second pipeline",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-01"
}
```

**aicontracts** (repo `pyyush/agentcontracts`) -- declarative **YAML agent contracts** for coding agents: one `AGENT_CONTRACT.yaml` declares what the agent may read/write/run/spend (`effects.authorized` fail-closed for filesystem/shell/tools/network/state_writes; token/tool/shell/duration budgets; deterministic postconditions). Optional SDK adapters (Claude Agent SDK PreToolUse deny, OpenAI Agents, LangChain) + **CI `aicontracts check-verdict`** on durable `verdict.json` (`pass|warn|blocked|fail`) so merges cannot go green on blocked/fail. Framework-agnostic core; GitHub Action. **PyPI `aicontracts==0.2.0`** (Apache-2.0; alpha); repo preparing advertised 1.0.0 — do not treat 1.0 as shipped until PyPI + `v1.0.0` tag both exist. Tip `6f5d347c489b17c1c5773096b1f5b3d14a0d5c75`; 0★.

**Revvel hit:** pin an `AGENT_CONTRACT.yaml` for the `wr:code` / `deliver:*` coder so scope, shell allowlist, and postconditions (pytest/ruff green) refuse out-of-scope writes and red checks before merge — wire `check-verdict` next to existing CI, not a parallel orchestrator. Pair with **spec-guard** (hash-bound human Approve/Authorize), **contract-agent** (CEL tool/multi-turn refuse), **governspec** (YAML→artifacts + offline tests; not a runtime enforcer), **agentverify** (cassette replay). Prefer Apache-2.0 over AGPL **agentassert-abc** for proprietary spine.

**Honesty:** CAN-PARTIAL. Verified 2026-10-01 (America/Denver): GitHub `pyyush/agentcontracts` 200 (Apache-2.0 LICENSE); PyPI `aicontracts` 0.2.0 200; README states 1.0.0 not yet published. Runtime deny completeness depends on host hook surface — CI verdict is the total gate. Young (0★). Not a grammar mask engine.

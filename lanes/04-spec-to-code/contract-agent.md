# ContractAgent

```json
{
  "id": "contract-agent",
  "name": "ContractAgent",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/stefanosello/contract-agent",
    "https://pypi.org/project/contract-agent/"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "wr:code / spec-approved / deliver:* — compile behavioral invariants + tool schemas once into typed AST; CEL GuardInterceptor refuses illegal tool transitions without a second spine",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-23"
}
```

**Spec-as-Source** engine for tool-using agents: declarative `agent.contract.yaml` (tools, CEL invariants, scenarios) → typed Pydantic `ContractAST` → deterministic runtime guards via Google CEL (`cel-python`). `GuardInterceptor` fail-closes on invariant violations with differentiated actions (`InvariantViolationError` / block tool payload / `EscalationRequiredError`). Custom workflow CEL helpers (`workflow.called_before`, `workflow.call_count`, approvals). Zero-LLM Hypothesis fuzz + mutation fixtures in `specs/001-core-engine` (Hypothesis under `[dev]`). Python ≥3.11; CLI entry `contract-agent`; MIT in `pyproject.toml` (GitHub license field still null; no root LICENSE file yet). **PyPI `contract-agent==0.2.6` live** as of 2026-09-24. Related draft spec (not a separate finding): [agentcontract/spec](https://github.com/agentcontract/spec) (AgentContract 0.1.0-draft) — language-agnostic YAML contract shape; ContractAgent is the concrete CEL implementation we care about.

**Revvel hit:** map CEL invariants onto the existing WR label graph — compile once at `research:complete` → `wr:code` / `spec-approved`, then refuse illegal tool call sequences on `deliver:*`. Pair with **specd** (context compile), **spec-guard** (human Approve/Authorize hashes), **compiled-ai** (LLM out of control plane), **agentverify** (cassette CI on the same tool sequences). Do **not** stand up a parallel orchestrator.

**Honesty:** CAN-PARTIAL. Verified 2026-09-23 (America/Denver): GitHub `stefanosello/contract-agent` live (created 2026-09-23, Python); real tree `src/contract_agent/{core,runtime,cli,testing}` with `ast.py` / `parser.py` / `cel_engine.py` / `guards.py` / `context.py`; unit tests; `specs/001-core-engine/spec.md` live; `pyproject.toml` declares MIT + deps `pydantic` / `cel-python` / `typer` / `rich` / `pyyaml`. Re-verified 2026-09-24 (America/Denver): repo still live (0★); **PyPI `contract-agent` 0.2.6 published** (Homepage/Repository → same GitHub); description expanded to Spec-Driven Behavioral Contract & Verification Engine; GitHub `license` API still null / no root LICENSE. Pattern + library, not a drop-in for `orchestrate.js`.

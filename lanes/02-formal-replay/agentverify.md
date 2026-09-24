# agentverify

```json
{
  "id": "agentverify",
  "name": "agentverify",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/simukappu/agentverify",
    "https://pypi.org/project/agentverify/"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "deliver:* CI — pytest cassette replay of tool sequences / budgets / forbidden tools next to chronos-dst and unflake; no second orchestrator",
  "honesty": "CAN",
  "acquired": "2026-09-24"
}
```

**pytest for AI agents.** Deterministic regression layer: record real LLM/tool runs once as human-readable YAML cassettes, replay in CI with zero API cost, assert exact tool-call sequences (order / subsequence / set), step-level dataflow, tool outcomes/retries, token/cost/latency budgets, and **forbidden tools**. Adapters for LangChain, LangGraph, Strands, OpenAI Agents SDK; converters for raw OpenAI/Anthropic/Bedrock/Gemini/LiteLLM. PyPI `agentverify==0.4.0`; MIT; CI + coverage badges live.

**Revvel hit:** pin `deliver:*` tool graphs in pytest next to **chronos-dst** / **unflake** — cassette diffs in PRs when prompts or WR labels change; `assert_no_tool_call` for tools that must never fire after `spec-approved`. Pair with **contract-agent** (runtime CEL refuse) for defense-in-depth: contract refuses live, agentverify catches regressions in CI. Prefer over thinner `tool-call-replay` clones. Do **not** invent a parallel agent OS.

**Honesty:** CAN. Verified 2026-09-24 (America/Denver): GitHub `simukappu/agentverify` live (8★, MIT LICENSE, Python, created 2026-04-15); PyPI `agentverify` 0.4.0 live (Homepage/Repository → same GitHub; deps `pytest>=7`, `PyYAML`); README documents cassette replay + `assert_tool_calls` / `assert_cost` / `assert_no_tool_call`. Not near-metal decode; CI gate only — honesty CAN for that scoped job.

# agentverify

```json
{
  "id": "agentverify",
  "name": "agentverify",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/simukappu/agentverify",
    "https://pypi.org/project/agentverify/",
    "https://github.com/simukappu/agentverify/releases/tag/v0.5.0",
    "https://github.com/simukappu/agentverify/blob/main/CHANGELOG.md"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "deliver:* CI — pytest cassette replay of tool sequences / budgets / forbidden tools next to chronos-dst and unflake; no second orchestrator. Pin >= 0.5.0: before it, calls a cassette could not replay (streaming, Responses API, embeddings, async Anthropic/Gemini) silently reached the real provider during 'replay'; credentials passed as call args could land in cassettes",
  "honesty": "CAN",
  "acquired": "2026-09-24",
  "updated": "2026-10-21"
}
```

**pytest for AI agents.** Deterministic regression layer: record real LLM/tool runs once as human-readable YAML cassettes, replay in CI with zero API cost, assert exact tool-call sequences (order / subsequence / set), step-level dataflow, tool outcomes/retries, token/cost/latency budgets, and **forbidden tools**. Adapters for LangChain, LangGraph, Strands, OpenAI Agents SDK; converters for raw OpenAI/Anthropic/Bedrock/Gemini/LiteLLM. PyPI `agentverify==0.4.0`; MIT; CI + coverage badges live.

**Revvel hit:** pin `deliver:*` tool graphs in pytest next to **chronos-dst** / **unflake** — cassette diffs in PRs when prompts or WR labels change; `assert_no_tool_call` for tools that must never fire after `spec-approved`. Pair with **contract-agent** (runtime CEL refuse) for defense-in-depth: contract refuses live, agentverify catches regressions in CI. Prefer over thinner `tool-call-replay` clones. Do **not** invent a parallel agent OS.

**Honesty:** CAN. Verified 2026-09-24 (America/Denver): GitHub `simukappu/agentverify` live (8★, MIT LICENSE, Python, created 2026-04-15); PyPI `agentverify` 0.4.0 live (Homepage/Repository → same GitHub; deps `pytest>=7`, `PyYAML`); README documents cassette replay + `assert_tool_calls` / `assert_cost` / `assert_no_tool_call`. Not near-metal decode; CI gate only — honesty CAN for that scoped job.

**Update 2026-10-19:** **agentverify 0.5.0** (PyPI 2026-10-17 19:14 MDT; GitHub release 19:15 MDT, "Replay never reaches the real API, credential redaction"). Fix-first release:

- **Replay no longer reaches the real API.** Calls a cassette cannot replay (streaming, the Responses API, embeddings, async Anthropic and Gemini clients) now raise `CassetteUnsupportedCallError` instead of calling the provider. Before 0.5.0 a "replayed" test could quietly make a live call, which breaks both the zero-cost and the determinism claim. Tests that made live non-chat calls during replay must move them outside the cassette.
- **Credentials passed as call arguments are redacted** from cassettes (`api_key=`, `x-api-key` header). Cassettes recorded on older versions with credentials passed that way should be checked before they are committed.
- OpenAI Agents SDK tool failures are now detected, so `assert_no_tool_errors` / `assert_tool_invocation_succeeded` no longer pass on them.
- `contains=` takes a list, `case_sensitive=False`; Python 3.15 and openai 3.x in CI.

**Revvel hit (2026-10-19):** pin `agentverify>=0.5.0` for any deliver:* replay test; the new exception is exactly the fail-closed behaviour a CI replay gate needs (a cassette miss is an error, not a network call). If cassettes were already recorded, grep them for keys before committing.

**Honesty (2026-10-19):** CAN. Verified 2026-10-19 (America/Denver): PyPI JSON (0.5.0, MIT), GitHub release v0.5.0 body read, release page 200.

**Update 2026-10-21:** **agentverify 0.6.0** (PyPI 2026-10-20 22:42 MDT; CHANGELOG dated 2026-10-21). Adds record/replay for the **async** Anthropic, Gemini and LiteLLM clients and the **OpenAI Responses API** (so the OpenAI Agents SDK works on its default model), plus **multi-agent handoff assertions** (`assert_handoffs`, `assert_no_handoff`, `assert_step(agent=...)`). Fixes: replayed multi-turn tool calls keep their recorded ids (was `call_0`), replayed `tool_results` hold only the step's own results, LiteLLM replay returns `litellm.ModelResponse`, Bedrock replay omits missing `usage`. **Breaking:** `from_openai_agents` now includes handoff items and starts a new step when the acting agent changes (multi-agent runs gain steps and tool calls, so step-index assertions shift), and **overlapping LLM calls while recording raise `CassetteUnsupportedCallError`** because their order varies run to run.

**Revvel hit (2026-10-21):** the overlap refusal is the right determinism rule for deliver:* cassettes (a concurrent recording is not replayable in a fixed order). `assert_no_handoff` is a cheap check that a coder run did not hand off to an agent it should not reach. Pin `==0.6.0` once existing cassettes and step assertions are re-run; stay on `>=0.5.0,<0.6` until then.

**Honesty (2026-10-21):** CAN. Verified 2026-10-21 (America/Denver): PyPI JSON 0.6.0 (MIT, upload 2026-10-21 04:42 UTC), `CHANGELOG.md` on `main` read raw. GitHub release page for v0.6.0 not checked (API budget).

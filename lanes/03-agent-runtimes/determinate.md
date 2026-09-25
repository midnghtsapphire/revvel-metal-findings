# determinate

```json
{
  "id": "determinate",
  "name": "determinate",
  "lane": "03-agent-runtimes",
  "status": "watching",
  "urls": [
    "https://github.com/cahaseler/determinate",
    "https://www.npmjs.com/package/determinate"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "State-gated next-action with constrained structured output \u2014 shrinks illegal tool picks on the wr:code / deliver:* loop without owning the orchestrator",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-25"
}
```

**determinate** \u2014 TypeScript **decision engine** (not a full agent framework). Treats the LLM as a next-action predictor: each `nextAction()` filters tools to those valid in the current state, builds a constrained output schema so the model **cannot** emit an illegal action, budgets context per section, and returns one validated action. No append-only chat history inside the library; you own the loop and side effects. Providers: OpenAI / Anthropic / vLLM / OpenRouter (uses their structured-output / constrained-decoding surfaces). npm `determinate@3.7.1` (published 2026-09-22); MIT; Node \u226522; bun tests + biome.

**Revvel hit:** on the openrouter-coder / labeler loop, gate the legal next WR label or tool by **state** (e.g. only `wr:code` after `spec-approved`) via schema constraint rather than prompt hope. Pair with **contract-agent** (runtime CEL refuse) and **agentverify** (cassette CI). Prefer over inventing another agent OS \u2014 determinate explicitly does **not** own the loop. Overlaps **openhands** watching lane; keep watching until a concrete insertion point in `engines/` is proven.

**Honesty:** CAN-PARTIAL. Verified 2026-09-25 (America/Denver): GitHub `cahaseler/determinate` live (6\u2605, MIT, TS, pushed 2026-09-22); npm `determinate` **3.7.1** live (Homepage \u2192 same GitHub; license MIT). Not near-metal decode (delegates masks to provider/vLLM structured outputs). Application-layer determinism only \u2014 honesty CAN-PARTIAL for that scoped job.

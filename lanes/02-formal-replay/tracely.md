# tracely

```json
{
  "id": "tracely",
  "name": "Tracely (trace-native CI gate for AI agents)",
  "lane": "02-formal-replay",
  "status": "watching",
  "urls": [
    "https://github.com/jwuthri-cloud/Tracely-ai",
    "https://pypi.org/project/tracelyai-sdk/"
  ],
  "license": "MIT",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Borrow the fail-to-pass replay case only: when a wr:code / deliver:* run fails, freeze its recorded inputs and tool/model outputs as a fixture that must fail on the old code and pass on the fix, and replay it offline in the existing check. Do not adopt the platform (that would be a second pipeline).",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-29"
}
```

**Tracely** (`jwuthri-cloud/Tracely-ai`, MIT; SDK on PyPI as `tracelyai-sdk` 0.0.1, uploaded 2026-10-12 13:12 MDT; repo created 2026-10-11, ~1.2k stars and 141 forks by 2026-10-29) bills itself as trace-native CI for agents: production trace → failure detection → regression test → CI gate → alert. A failing trace is promoted to a **hermetic case**: recorded input plus tool and LLM outputs bundled as fixtures, with a **fail-to-pass contract** (the case must fail on the old code and pass on the fix). The suite replays in CI against those fixtures (deterministic, offline, no API keys, no model spend), and `tracely gate` exits non-zero, posts a commit status and upserts a PR comment.

Caveats from the README:
- Hermetic replay only works if the agent routes tool/model calls through the SDK's `call_tool` / `call_llm` seam.
- The gate talks to a running Tracely API (ingest key + API URL); self-hosting means API, worker, UI, Postgres, ClickHouse, Redis and MinIO.
- The default `dev` auth mode is open, and the dev ingest key is `tracely_dev_key`.
- The README's GitHub Action is referenced at `@master`; pin a SHA (or lock it with gh-actions-lock) if anything is ever borrowed.
- No GitHub releases; only a `sdk-v0.0.1` tag.

**Revvel hit:** the fail-to-pass contract is the useful idea for wr:code: a bug found in a deliver:* run becomes a frozen case that blocks any PR reintroducing it. It is the same family as **agentverify** cassettes, **chronicle** cut-point replay and **agrepl** (02). Borrow the case format idea into the existing check. The full platform is a second pipeline plus a heavy data stack, so no adoption.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-29 (America/Denver): GitHub repo page 200, repo API (license MIT, created date, stars), tags and releases API (no releases), README read in raw (not cloned), PyPI JSON for `tracelyai-sdk`. Star count grew fast for an 18-day-old repo; not independently assessed. Nothing run.

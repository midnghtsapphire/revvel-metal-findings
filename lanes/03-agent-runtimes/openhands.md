# OpenHands

```json
{
  "id": "openhands",
  "name": "OpenHands",
  "lane": "03-agent-runtimes",
  "status": "watching",
  "urls": [
    "https://docs.all-hands.dev/",
    "https://github.com/OpenHands/OpenHands",
    "https://github.com/OpenHands/software-agent-sdk"
  ],
  "license": "per-repo, do not assume one SPDX",
  "metal": 3,
  "determinism": 2,
  "revvel_hit": "Already on the README fallback chain. Gate on spec-approved + wr:code. Do not open a second coder path.",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Code-first agent (Canvas + Software Agent SDK + Agent Server). Already named in revvel-standards: openrouter → openhands → human. `.github/workflows/openhands-resolver.yml` exists.

**Revvel hit:** keep it as fallback after OpenRouter. Delivery Mode `proposal-first` vs `build-direct`. Do not let it fire on a research-only WR. Pair with the missing #15507 handoff so it receives a task list, not a novel.

**Status watching:** agent, not a grammar. Useful once the label bridge exists.

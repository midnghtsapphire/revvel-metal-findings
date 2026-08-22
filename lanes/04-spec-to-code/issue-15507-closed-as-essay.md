# #15507 closed as an essay

```json
{
  "id": "issue-15507-closed-as-essay",
  "name": "Spec-to-action bridge closed without the workflow",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/midnghtsapphire/revvel-standards/issues/15507",
    "https://github.com/midnghtsapphire/revvel-standards/pull/15572",
    "https://github.com/midnghtsapphire/revvel-standards/blob/main/wr/pending/03-spec-to-action-bridge.md"
  ],
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "Land spec-to-action-bridge.yml + a grammar-caged task list. Do not open another WR about the WR.",
  "honesty": "CAN",
  "acquired": "2026-08-22"
}
```

Owner-written gap: fleet writes a spec, cannot put it in action. Required: on `research:complete`, extract DoD, emit file/command task list, apply `wr:code` or `wr:jules`, timeout → `lifecycle:stuck` + `needs-human`.

Closed `completed` with two PRs (#15572 merged, #15524 closed). Merged payload is a WR markdown file. Files named in that WR (`spec-to-action-bridge.yml`, `extract_tasks.py`) 404 on `main` today.

This is the receipt that the findings tree is not theoretical. The next metal we add (XGrammar/GBNF on the handoff JSON, DSPy compile of the labeler, DST on the label graph) goes *here*, not into another research packet.

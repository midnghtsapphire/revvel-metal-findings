# Spec Guard

```json
{
  "id": "spec-guard",
  "name": "Spec Guard",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/jpstone/spec-guard",
    "https://www.npmjs.com/package/@jpstone/spec-guard"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "MCP + CLI governance: hash-bound human Approve / Authorize / Complete gates so agents cannot self-approve or skip spec-approved before wr:code",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-09-18"
}
```

Local governance layer for agentic implementation workflows. Ships as `@jpstone/spec-guard` (npm **3.1.0**, MIT) with `spec-guard` CLI and `spec-guard-mcp` MCP server. Work is a typed **Work Packet** (intent, acceptance criteria, plan, scope, dependencies) that must pass three **human** gates — Approve (plan), Authorize (start coding), Complete (done + proven evidence) — each hash-bound to the exact content reviewed. Edit after approval and the gate goes stale. Role separation (coordinator / implementer / reviewer / validator) plus an edit-gate hook blocks anyone but the delegated implementer from touching product code. Frozen JSON-Schema **contracts** are content-hashed and travel in git under `.spec-guard/`.

**Revvel hit:** closest live drop-in for making `spec-approved` → `wr:code` → `deliver:*` **structural** rather than advisory. Wire the MCP into the existing handoff agent; do not invent a second pipeline — Spec Guard owns the packet/contract store beside the WR, not a parallel coder path.

**Honesty:** CAN-PARTIAL. GitHub `jpstone/spec-guard` + npm `@jpstone/spec-guard@3.1.0` verified live 2026-09-18. Young (0★). Requires Node ≥ 24. Human-in-the-loop by design — not a fully automatic gate; Completeness still needs passing evidence commands you configure. Not a grammar mask engine.

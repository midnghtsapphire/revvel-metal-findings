# specgate

```json
{
  "id": "specgate",
  "name": "SpecGate",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/thanhtung2693/specgate"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 2,
  "revvel_hit": "spec-approved → deliver:* — humans approve an exact artifact version, the coder reads only that version as a governed Context Pack via the specgate CLI, and `specgate delivery submit` runs report → gates → review against the approved acceptance criteria",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-07"
}
```

**SpecGate** -- local-first control plane for AI-assisted delivery. An authoring tool (OpenSpec, Spec Kit, Kiro, plain Markdown) publishes a versioned artifact; SpecGate resolves policy and readiness gates; a human approves the exact version when policy requires it; the coding agent pulls the approved Context Pack through the `specgate` CLI; delivery evidence comes back through `specgate delivery submit` for verdicts, reconciliation, and audit. Ships plugin files for Claude Code, Cursor, and Codex. Stack: Go doc-registry (artifacts, versions, policy, evidence, REST + MCP), Python/LangGraph agents (governance ops, model-judged gates, delivery review), React UI, Go/Cobra CLI. Apache-2.0; latest tag **v0.2.5** (2026-09-17); tip `0f1dabb545be355441911cc5906d44d106208be0` (2026-10-04); ~6★. GitHub/Linear mirrors and webhook delivery evidence are still on the roadmap.

**Revvel hit:** the shape is exactly the `spec-approved` → `deliver:*` handoff (approved version pinned, coder context derived from it, delivery checked against its ACs). Worth borrowing the "approve an exact version, hand the coder only that version" idea for the WR body.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-07 (America/Denver): repo live, Apache-2.0. It is a multi-service stack (Go registry + Python LangGraph + UI) and several gates are model-judged, so it is not deterministic and would amount to a second pipeline if adopted whole. Prefer **spec-guard** / **linebreak-gate** for the human gate and **cadence** / **mcp-gate** for delivery checks; revisit if the GitHub integration lands and gates can run deterministic-only.

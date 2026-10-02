# verax

```json
{
  "id": "verax",
  "name": "Verax (@verax-ai/body)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/verax-ai/verax",
    "https://www.npmjs.com/package/@verax-ai/body",
    "https://verax-ai.com"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* — MCP policy gate + signed COSE decision records + effect reconciliation before tool runs; operator approve for held calls",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-02"
}
```

**Verax** (`@verax-ai/body`) -- MCP “accountable agent body”: every tool call passes a policy gate and leaves a **signed decision record** (COSE_Sign1 Ed25519) before anything runs; effects reconcile against records afterward. Refusals recorded same as approvals; held calls wait for `verax approve` on-machine. `verax verify` reads the ledger offline (signatures + chain). Packages: `@verax-ai/body`, `@verax-ai/proxy`, `@verax-ai/inventory`. Apache-2.0; npm **0.4.1** (~499 weekly downloads); tip `4d17702c7beb2e5d9cd8166dae833d47916acb6f` (pushed 2026-10-02); 0★ repo but active.

**Revvel hit:** optional fail-closed policy shell around tool/MCP side-effects for high-stakes `deliver:*` paths — signed audit beside existing handoff, not a second WR pipeline. Heavier than **agent-gate** (checklist) / **aicontracts** (YAML effects); pair with **homi-gate** for CI shape checks. Requires issuer/JWKS/policy config (no default token).

**Honesty:** CAN-PARTIAL. Verified 2026-10-02 (America/Denver): GitHub Apache-2.0 + npm `@verax-ai/body` 0.4.1 live; STATUS.md is the capability contract — do not claim beyond it. Install boundary is admin-owned copy for real threat model; `verax init --local` is not that boundary. Young (0★).

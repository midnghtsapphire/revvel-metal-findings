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
    "https://verax-ai.com",
    "https://github.com/verax-ai/verax/releases/tag/v0.5.0",
    "https://github.com/verax-ai/verax/releases/tag/v0.5.1"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* — MCP policy gate + signed COSE decision records + effect reconciliation before tool runs; operator approve for held calls. Pin >= 0.5.1: 0.5.0 makes policy parsing fail closed (unknown keys refused; `message.send` rules must carry `egress: true`)",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-02",
  "updated": "2026-10-12"
}
```

**Verax** (`@verax-ai/body`) -- MCP “accountable agent body”: every tool call passes a policy gate and leaves a **signed decision record** (COSE_Sign1 Ed25519) before anything runs; effects reconcile against records afterward. Refusals recorded same as approvals; held calls wait for `verax approve` on-machine. `verax verify` reads the ledger offline (signatures + chain). Packages: `@verax-ai/body`, `@verax-ai/proxy`, `@verax-ai/inventory`. Apache-2.0; npm **0.4.1** (~499 weekly downloads); tip `4d17702c7beb2e5d9cd8166dae833d47916acb6f` (pushed 2026-10-02); 0★ repo but active.

**Revvel hit:** optional fail-closed policy shell around tool/MCP side-effects for high-stakes `deliver:*` paths — signed audit beside existing handoff, not a second WR pipeline. Heavier than **agent-gate** (checklist) / **aicontracts** (YAML effects); pair with **homi-gate** for CI shape checks. Requires issuer/JWKS/policy config (no default token).

**Honesty:** CAN-PARTIAL. Verified 2026-10-02 (America/Denver): GitHub Apache-2.0 + npm `@verax-ai/body` 0.4.1 live; STATUS.md is the capability contract — do not claim beyond it. Install boundary is admin-owned copy for real threat model; `verax init --local` is not that boundary. Young (0★).

**Update 2026-10-12:** npm `@verax-ai/body` is now **0.5.1** (published 2026-10-11 20:54 MDT; 0.4.2–0.4.8 and 0.5.0 landed 2026-10-02 → 2026-10-11 MDT). **0.5.0 (npm 2026-10-11 18:35 MDT) is a breaking, stricter-fail-closed release:** a policy with a key the parser does not know (document, rule, `spend`, `limits`) no longer loads; a `message.send` rule must carry `egress: true` and every top-level `egress` host list must be read by a marked rule, otherwise the policy is refused (`policy-rule-egress-unmarked:<id>`, `policy-egress-unused`) — up to 0.4.8 such a rule loaded and its host was **not checked**; a downstream child message over 10 MiB is refused and the child detached. Automatic anchoring and signed start rows shipped in 0.5.0. 0.5.1 is a demo-prompt fix plus threat-model doc correction, no other source change; also published as `@verax-ai/proxy` / `@verax-ai/inventory` 0.5.1, Docker `veraxai/verax:0.5.1`, MCP registry `io.github.verax-ai/verax` 0.5.1. Action: any trial policy written against 0.4.x must be re-validated on 0.5.1 (move comments out of the file, mark egress rules); pin `@verax-ai/body@0.5.1`. Verified 2026-10-12 via npm registry + GitHub release notes; repo still Apache-2.0, not archived.

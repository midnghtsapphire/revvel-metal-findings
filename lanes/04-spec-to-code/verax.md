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
    "https://github.com/verax-ai/verax/releases/tag/v0.5.1",
    "https://github.com/verax-ai/verax/releases/tag/v0.6.0",
    "https://github.com/verax-ai/verax/releases/tag/v0.6.1"
  ],
  "license": "Apache-2.0",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "wr:code / deliver:* — MCP policy gate + signed COSE decision records + effect reconciliation before tool runs; operator approve for held calls. Pin >= 0.6.1: 0.6.0 escapes ledger/approval text shown to the operator (terminal-escape and invisible-character spoofing), adds signed pinned tool definitions for downstream children; 0.6.1 stops reconcile/ledger readers trusting amounts from the unsigned approval queue. 0.5.0's fail-closed policy parsing still applies",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-02",
  "updated": "2026-10-19"
}
```

**Verax** (`@verax-ai/body`) -- MCP “accountable agent body”: every tool call passes a policy gate and leaves a **signed decision record** (COSE_Sign1 Ed25519) before anything runs; effects reconcile against records afterward. Refusals recorded same as approvals; held calls wait for `verax approve` on-machine. `verax verify` reads the ledger offline (signatures + chain). Packages: `@verax-ai/body`, `@verax-ai/proxy`, `@verax-ai/inventory`. Apache-2.0; npm **0.4.1** (~499 weekly downloads); tip `4d17702c7beb2e5d9cd8166dae833d47916acb6f` (pushed 2026-10-02); 0★ repo but active.

**Revvel hit:** optional fail-closed policy shell around tool/MCP side-effects for high-stakes `deliver:*` paths — signed audit beside existing handoff, not a second WR pipeline. Heavier than **agent-gate** (checklist) / **aicontracts** (YAML effects); pair with **homi-gate** for CI shape checks. Requires issuer/JWKS/policy config (no default token).

**Honesty:** CAN-PARTIAL. Verified 2026-10-02 (America/Denver): GitHub Apache-2.0 + npm `@verax-ai/body` 0.4.1 live; STATUS.md is the capability contract — do not claim beyond it. Install boundary is admin-owned copy for real threat model; `verax init --local` is not that boundary. Young (0★).

**Update 2026-10-12:** npm `@verax-ai/body` is now **0.5.1** (published 2026-10-11 20:54 MDT; 0.4.2–0.4.8 and 0.5.0 landed 2026-10-02 → 2026-10-11 MDT). **0.5.0 (npm 2026-10-11 18:35 MDT) is a breaking, stricter-fail-closed release:** a policy with a key the parser does not know (document, rule, `spend`, `limits`) no longer loads; a `message.send` rule must carry `egress: true` and every top-level `egress` host list must be read by a marked rule, otherwise the policy is refused (`policy-rule-egress-unmarked:<id>`, `policy-egress-unused`) — up to 0.4.8 such a rule loaded and its host was **not checked**; a downstream child message over 10 MiB is refused and the child detached. Automatic anchoring and signed start rows shipped in 0.5.0. 0.5.1 is a demo-prompt fix plus threat-model doc correction, no other source change; also published as `@verax-ai/proxy` / `@verax-ai/inventory` 0.5.1, Docker `veraxai/verax:0.5.1`, MCP registry `io.github.verax-ai/verax` 0.5.1. Action: any trial policy written against 0.4.x must be re-validated on 0.5.1 (move comments out of the file, mark egress rules); pin `@verax-ai/body@0.5.1`. Verified 2026-10-12 via npm registry + GitHub release notes; repo still Apache-2.0, not archived.

**Update 2026-10-19:** npm `@verax-ai/body` is now **0.6.1** (npm 2026-10-17 10:19 MDT; GitHub release v0.6.1 10:26 MDT, commit `90f9b066a394`); **0.6.0** landed 2026-10-16 (npm 08:52 MDT, release 09:07 MDT, commit `a7264bdcf565`). Both also published as `@verax-ai/proxy` / `@verax-ai/inventory`, Docker `veraxai/verax`, MCP registry `io.github.verax-ai/verax`. License still Apache-2.0 (npm metadata).

- **0.6.0 security:** `verax verify` printed ledger text raw, so a ref in the unsigned `index.jsonl` could carry terminal escapes or a line break that printed a fake `VERIFIED` line above the real `NOT VERIFIED`; all printed lines now escape those code points (#224). The `verax approve` prompt now also escapes variation selectors, zero-width/combining/unassigned code points, so a held call cannot hide text from the operator (#223). **New:** **pinned tool definitions for downstream children** (`pins: "sha256:<digest>"` + `verax downstream pin`): a child that changes a pinned description or schema stops the body at its next start, and the signed start row names each child's manifest for `verax verify` (#218); an optional passkey **operator door** for approving held calls from another device (off unless `VERAX_OPERATOR_DOOR` is set; loopback listener behind your own TLS; release notes say it has had code reviews but no independent attack round); `verax operator list/remove` with signed removal records (#210, #217, #225). Downstream start refusal now exits 78.
- **0.6.1 security:** `verax reconcile --channel card` and the panel's ledger API read an approved spend's amount/currency/payee from the **unsigned** `approvals.jsonl` queue; a row edited after approval was reported as matched. A queue row now lends those fields only when its tool-name+arguments hash equals the `requestHash` on the signed decision; otherwise "unknown" (#229). Approving itself was not affected (it already checked the queue row against the signed request). Bad `VERAX_POLICY_FILE` paths now exit 78 with one line.

**Revvel hit (2026-10-19):** the 0.6.0 downstream pin is the same idea as **agentgate**'s lock and **mcp-hangar**'s digest pin, but enforced at start and recorded in the signed ledger. The 0.6.1 fix is the general lesson for any deliver:* receipt: only read approved values from the signed record, never from the mutable queue next to it. Pin `@verax-ai/body@0.6.1` for any trial.

**Honesty (2026-10-19):** CAN-PARTIAL. Verified 2026-10-19 (America/Denver) via npm registry JSON (versions + times), GitHub releases API bodies for v0.6.0 and v0.6.1, release pages 200. Not run.

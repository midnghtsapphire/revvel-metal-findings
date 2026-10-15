# agt-approval-protocol

```json
{
  "id": "agt-approval-protocol",
  "name": "Agent Governance Toolkit ADR-0030: Action-Bound, Fail-Closed Approval Protocol (microsoft/agent-governance-toolkit)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://microsoft.github.io/agent-governance-toolkit/adr/0030-action-bound-approval-protocol/",
    "https://github.com/microsoft/agent-governance-toolkit/blob/main/docs/adr/0030-action-bound-approval-protocol.md",
    "https://github.com/microsoft/agent-governance-toolkit/tree/main/agent-governance-python/agent-mesh/src/agentmesh/governance/approval_protocol",
    "https://github.com/microsoft/agent-governance-toolkit"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Written contract for the deliver:* consent record: approval binds to SHA-256(RFC 8785 JCS(action binding)) + policy_version + approval_chain_version; require_approval is a suspended state (not allow, not deny); execution-time revalidation of digest/policy/chain/expiry/one-time consumption in the same transaction that starts the side effect; timeout, transport failure, malformed or unauthenticated approver = deny; LLM output is advisory only and can never resolve a stage. Borrow the schema and the 7-point execute check; do not adopt the toolkit as a second pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-15"
}
```

**ADR-0030** in Microsoft's **Agent Governance Toolkit** (AGT; MIT; ~6.4k★; repo created 2026-03-02, pushed 2026-10-15 04:30 MDT). Status **accepted** (ADR dated 2026-06-11; "mark ADR-0030 accepted" commit `156a2c6a1aef`, 2026-09-13 13:06 MDT; `last_reviewed: 2026-09-06`). It replaces AGT's ad-hoc approval callbacks with one versioned protocol:

- **Outcomes:** `allow` / `deny` / `require_approval`; `require_approval` is a durable *suspended* decision, never collapsed into allow or an ordinary deny.
- **Action binding:** `{schema_version, operation, agent_id, subject_id, target{tool_name, tool_schema_version, resource}, parameters}` → `action_digest` = lowercase hex SHA-256 of the RFC 8785 JCS bytes. The execution boundary must be able to recompute it.
- **Four objects:** PolicyDecision → ApprovalRequest (expiry, `fail_closed_on_timeout: true`) → hash-linked append-only ApprovalChainEntry (`input_digest`, `previous_entry_digest`, `entry_digest`) → ApprovalResolution. Only a resolution with `outcome: allow` releases execution; individual votes are not execution tokens.
- **Execution-time check (atomic):** resolution is terminal allow; not expired/cancelled/denied/consumed; current digest == approved digest; current policy version == approved; chain version == approved; chain entries + identities valid; one-time consumption. For irreversible or externally visible actions, consume the approval **in the same transaction/idempotency boundary that starts execution** (no two workers reusing one approval).
- **Identity/transport:** webhook is a transport, not an approver identity; body-supplied approver strings are rejected unless bound to authenticated transport; timeout auto-approve is deprecated and rejected in strict mode.
- **LLM:** may annotate; cannot satisfy a human stage or produce a terminal resolution (ADR-0004 keeps model inference out of enforcement).

Implementation on `main`: Python `agentmesh/governance/approval_protocol/` (`models.py`, `coordinator.py`; foundation PR #3015, 2026-06-14 20:04 MDT, "purely additive, nothing wired into the policy evaluator yet"), fail-closed fixes #3448 (zero required stages → deny, 2026-07-30) and #3587 (duplicate/negative `stage_index` let one approval satisfy two stages; confirmed exploitable, fixed 2026-09-14), plus .NET `AgentGovernance/Approvals/ApprovalCoordinator.cs` (`action_digest_mismatch` reason code). Go and TypeScript parity ports are referenced in those commits.

**Revvel hit:** revvel-standards already has the gates (**spec-guard** for spec-approved, **agent-approval-check** for merge, **hashgate** / **notary-mcp** for side-effect consent). What it lacks is one *written* record format for "this exact deliver:* action was approved under this policy version". ADR-0030 is the most complete public spec of that record and its execute-time check list. Use it as the reference when writing the deliver:* approval schema next to `schemas/state.schema.json` (insertion point 2). Do not run AGT as a second control plane.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-15 (America/Denver): GitHub Pages ADR page fetched in full; repo web + ADR blob 200; GitHub API (MIT, not archived); `coordinator.py` raw 200; commit history for `approval_protocol/` read via API. **Not in any released package checked:** PyPI `agentmesh-platform` latest is **3.7.0** (2026-05-18), whose wheel ships only the older `agentmesh/governance/approval.py`; NuGet `Microsoft.AgentGovernance` **5.0.0** (2026-07-27) DLL has no `ApprovalCoordinator` / `ApprovalResolution` types; in-tree `pyproject.toml` says 5.0.0 (unreleased); GitHub releases latest v4.1.0 (2026-06-09). Migration steps 2–6 (wiring into the evaluator, MCP gateway, webhook replacement) are not confirmed done. Heavy, broad toolkit; only the protocol is in scope. Move to active if a release ships the coordinator.

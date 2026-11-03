# mcp-destructive-approval

```json
{
  "id": "mcp-destructive-approval",
  "name": "When Neither Side Confirms: destructive tool approval across MCP servers and hosts",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.02527"
  ],
  "license": "UNKNOWN (no code released)",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "Rule for any MCP gate on the coder (mcp-gate / mcp-hangar / verax): require human approval for every tool not annotated read-only or non-destructive, enforced in the host/gateway, and never fall back to a flag the model can set. Measured: that rule cuts unapproved destructive pairs from 60.7% to 5.4%, while relying on server elicitation leaves 56.7%. Paper only.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-03"
}
```

**When Neither Side Confirms: Destructive Tool Approval Across MCP Servers and Hosts** (Yao, Yang, Wang, Zhou, Ye). arXiv **2611.02527** v1, submitted 2026-11-01 21:57 MST (cs.CR). No code or artifact link in the abstract or HTML version.

Authors' numbers (source-code measurement): in a 1,000-repository sample of the official MCP registry, ~90% (95% CI 82-95) of destructive tools have no server-side confirmation, and most servers that use elicitation proceed, or fall back to a model-settable flag, when the host cannot relay the question. 32 of 41 popular hosts / agent SDKs (16 of 25 applications) have no approval step by default. Pairing destructive tools with these apps: 60.7% have no enforced human approval by default. Through four agent SDKs, four of five low-cost models executed an injected deletion in 479 of 960 runs. Host prompting for **every tool not annotated read-only or non-destructive** would drop the unapproved share to **5.4%**; universal elicitation support would leave **56.7%**.

**Revvel hit:** settles where the deliver:* approval lives: in the host/gateway on the coder's MCP path (the existing mcp-gate / mcp-hangar policy), default-hold on any tool lacking `readOnlyHint` / non-destructive annotation, never a model-settable confirm flag. mcp-gatehouse 0.5.0's elicitation approver is useful only with a host that relays it, and its fallback must deny. No second pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-03 (America/Denver): arXiv export API metadata + abstract, abs page 200, HTML version checked for code links (none). Results are the authors'.

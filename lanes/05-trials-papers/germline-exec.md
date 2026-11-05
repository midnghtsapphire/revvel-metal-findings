# germline-exec

```json
{
  "id": "germline-exec",
  "name": "Signed, Sealed, Leaked: germline execution for MCP toolchains",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.06585",
    "https://arxiv.org/html/2611.06585v1"
  ],
  "license": "n/a (paper; no code link found)",
  "metal": 3,
  "determinism": 4,
  "revvel_hit": "Signing and allowlists do not stop a signed MCP tool from leaking data to a policy-allowed destination. Germline execution runs each tool call in an ephemeral fork of a data-free process that receives only the data authorized for that call's destination. For revvel-standards: when a deliver:* coder gets MCP tools, scope the data each call can see per WR, not just which tools are allowed. Reference only; enforce through the existing mcp-hangar / verax gate, no new pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-05"
}
```

**Signed, Sealed, Leaked: Trust Beyond Signature for MCP Toolchains** (Aun et al.). arXiv **2611.06585** v1, submitted 2026-11-04, 24 pages. A signed, policy-compliant MCP tool still leaked data to an allowed destination, and Meta's `facebook/mcpguard-dynamic` (cited baseline, MIT) did not stop it in any trial. The paper's fix, "germline execution", forks each invocation from a data-free germline process and hands it only the data authorized for its destination, so what malicious code can disclose is bounded by its copy. Authors' numbers: 0 unauthorized disclosures across 153 runs versus 5.9-74.5% under baseline defenses; a single-copy invocation costs 10-49 ms, 2-28x faster than restarting the tool.

**Revvel hit:** pairs with **delegated-scope** (per-WR tool list) and **mcp-hangar** / **verax** (gate + ledger): the missing piece is per-call data scope. Fork-per-call is close to the metal (process fork, copy-on-write) and cheap enough for the coder loop. Watch for code before any trial.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-05 (America/Denver): arXiv export API abstract and the HTML full text (GitHub links found: only the cited baselines `facebook/mcpguard-dynamic` and `microsoft/agent-governance-toolkit`; no artifact link). `facebook/mcpguard-dynamic` repo API: MIT. Not run. Results are the authors'.

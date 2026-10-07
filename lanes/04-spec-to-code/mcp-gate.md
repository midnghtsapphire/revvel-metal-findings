# mcp-gate

```json
{
  "id": "mcp-gate",
  "name": "mcp-gate (Execution Governance)",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://www.npmjs.com/package/@11ai/mcp-gate",
    "https://github.com/11-11AI/execution-governance"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "wr:code / deliver:* — one-line stdio proxy in front of any MCP server the coder uses; every tools/call is checked against a policy file before forwarding, denied calls never reach the server, and every allow/deny is an Ed25519-signed, SHA3-512-chained receipt verifiable offline with eg-verify",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-07"
}
```

**mcp-gate** -- fail-closed stdio proxy that sits between any MCP client (Claude Code, Cursor, Claude Desktop) and any MCP server (filesystem, GitHub, databases). Each `tools/call` is evaluated against a YAML policy before it is forwarded; a denied call gets a JSON-RPC error and a signed receipt. Engine error, timeout, or malformed policy all deny; if the policy cannot load, the gate exits nonzero and the wrapped server never starts. A policy-check command runs the engine's own parser, catching undeclared `actionClass` names and uncompilable `argsPattern` regexes that would otherwise load as valid YAML and silently deny everything. Receipts are Ed25519-signed, SHA3-512-hashed, and chained; `eg-verify` checks the file offline. npm **@11ai/mcp-gate 0.4.2** (published 2026-09-17; first publish 2026-07-19); source in the `packages/mcp-gate` directory of 11-11AI/execution-governance, tip `f2efb313d113149c6ddc9656307a605a7619f8ea` (2026-09-17); Apache-2.0 LICENSE.

**Revvel hit:** a Node-native wrapper for the coder's MCP config, so `wr:code` tool calls are policy-checked deterministically without changing the coder or the servers. Put the write-scope rules (allowed paths, no secret material outbound, no dangerous shell) in the policy, and attach the receipt file to the `deliver:*` evidence. Same pipeline, one more wrapper; not a second pipeline. Overlaps **verax** (MCP policy gate + COSE ledger) and **agent-gate** (receipts); mcp-gate is the lightest drop-in of the three because it needs no code changes.

**Honesty:** CAN-PARTIAL. Verified 2026-10-07 (America/Denver): npm registry live at 0.4.2, repo live with Apache-2.0 LICENSE. Without a configured signing key a new key is generated per run, so receipts are not verifiable across restarts; set a persistent key. An optional hosted control plane (`EG_CONTROL_PLANE_URL`) exists; keep to the local policy file so the gate stays deterministic and offline. Young package; pin the version.

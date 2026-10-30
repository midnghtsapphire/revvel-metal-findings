# mcp-digest-vectors

```json
{
  "id": "mcp-digest-vectors",
  "name": "mcp-digest-vectors (known-answer vectors for MCP tool-definition pinning)",
  "lane": "02-formal-replay",
  "status": "watching",
  "urls": [
    "https://github.com/purysho/mcp-digest-vectors",
    "https://github.com/purysho/mcp-digest-vectors/blob/main/SPEC.md",
    "https://github.com/purysho/mcp-digest-vectors/blob/main/results/RESULTS.md",
    "https://github.com/modelcontextprotocol/modelcontextprotocol/issues/3452"
  ],
  "license": "MIT (vendored RFC 8785 test data Apache-2.0)",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "KAT for the coder's MCP tool pin: run whatever pins the tool surface (agentgate.lock, mcp-hangar digest pin) against these before/after tools/list vectors and expected digests; reject duplicate JSON keys and pin the full tool object, not the description. No release yet, so pin a commit SHA.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-30"
}
```

**mcp-digest-vectors** (`purysho/mcp-digest-vectors`, MIT; repo created 2026-10-29 09:25 MDT, 0 stars, no releases or tags; tip `4ec1041c1c`). Conformance vectors for "rug-pull" detection: an MCP server changes a tool definition after the client approved it. Each vector is a before/after `tools/list` pair with the verdict a pinning client must reach (45 vectors: 9 equal, 19 drift, 6 scope, 10 reject, 1 limit) and the known-answer digest under a draft scheme `mcp-tool-digest/v1-draft` (RFC 8785 JCS canonical JSON, SHA-256, full tool object in scope). It ships a stdlib-only Python reference, an independent Rust implementation that reproduces all 270 known answers, and a fixture MCP server plus runner for testing a real client.

Two results the repo reports (its own numbers, not re-run here): a parser that keeps the **last** duplicate key pins the safe text when a duplicated `description` puts the malicious value first, so duplicate keys must be rejected, not resolved; and a pin over the **description only** catches only 10 of 18 scored drift cases (it misses schema and annotation changes, including instructions hidden in a parameter's description), handles 6 of 10 parser differentials and 0 of 6 scope cases. It was written as input to MCP **SEP-3452** (tool-definition pinning), which upstream closed as completed on 2026-10-26 with the scheme still to be settled in working-group discussion.

**Revvel hit:** this is a test corpus, not a runtime. **agentgate** (`agentgate.lock` + `ci`) and **mcp-hangar** (`pin --check`) already pin the coder's tool surface; feed their pin step these vectors as a known-answer test so "the tool changed" fails CI for the right reasons, the same way **agent-evidence-vectors** is used for approval binding. Nothing to install in revvel-standards; no second pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-30 (America/Denver): repo page 200 and repo API (MIT, created date, no releases), README read through the API (category counts and results table), SPEC.md and results/RESULTS.md present (200), SEP-3452 issue page 200 (closed 2026-10-26). One day old, single author, digest scheme marked draft and may change. Vectors not run on the box.

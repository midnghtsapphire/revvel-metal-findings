# hashgate

```json
{
  "id": "hashgate",
  "name": "hashgate",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/Seppelllo/hashgate",
    "https://pypi.org/project/hashgate/",
    "https://pypi.org/project/hashgate/0.2.0/"
  ],
  "license": "Apache-2.0",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Claude Code PreToolUse gate for git push/merge/reset/rm and deploy commands: operator accepts a canonical payload hash; server re-derives from live state and refuses TOCTOU drift; agent cannot self-approve. Watching — borrow the pattern for deliver:* side effects beside Spec Guard's Work Packet gates.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-14"
}
```

**hashgate** -- fail-closed, hash-bound human approval for AI agent side effects (Apache-2.0). Agent proposes a gated action; operator reviews the exact payload (for `git push`: remote SHA + transported commits) and accepts its full canonical hash; on retry the server **re-derives** the payload from live state, compares hashes, then applies once (single-use, TTL). Agent-issued `accept`/`deny` is always blocked. Ships Claude Code PreToolUse hook (command-hook wrapper fail-closed if server down; direct HTTP is advisory), CLI (`hashgate pending|show|accept|deny`), and localhost operator web UI with typed 12-hex hash echo. Core library is dependency-free; optional `[server]` extra for FastAPI + SQLite. PyPI **0.2.0** (uploaded 2026-07-02 12:43 MDT); repo last push 2026-07-02 14:16 MDT; ~3★; Python ≥3.11; not archived.

**Revvel hit:** closest live pattern for binding *coder shell effects* (push/merge/deploy) to a human-approved state hash — complementary to **spec-guard** (Work Packet Approve/Authorize/Complete) and **agent-approval-check** (merge-side PR approvals). Do not invent a second pipeline: if wr:code's deliver path needs TOCTOU-safe push/merge consent, borrow hashgate's re-derive-then-compare accept order (or wire the hook only on the existing coder host). Prefer Spec Guard for `spec-approved`; this is for the concrete side-effect boundary.

**Honesty:** CAN-PARTIAL. Verified 2026-10-14 (America/Denver): GitHub API 200 (Apache-2.0, not archived), PyPI 0.2.0 live, README + `pyproject.toml` read. Stale since 2026-07-02 (~3 months, no newer release) — watching, not active. Local single-operator tool, not a sandbox (threat model is explicit). Crowded hash-approval niche (**notary-mcp**, InterLock, mcp-verified-approval); taken for Claude Code hook + live-state re-derivation on git/deploy, which those miss.

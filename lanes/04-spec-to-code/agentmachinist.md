# agentmachinist

```json
{
  "id": "agentmachinist",
  "name": "AgentMachinist (vscarpenter/AgentMachinist)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/vscarpenter/AgentMachinist",
    "https://github.com/vscarpenter/AgentMachinist/releases/tag/v0.20.0",
    "https://pypi.org/project/agentmachinist/",
    "https://agentmachinist.vinny.dev/architecture.md"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "Spec-approved -> execute handoff done the way wr:code wants it: Human Approval names the exact Spec commit; approval evidence is a `<!-- agentmachinist:approval sha=<40-hex head> -->` marker that only the workflow bot can mint after a fail-closed write/admin permission read (a human-typed marker is ignored; the label alone = 'approval pending'); any branch update makes approval stale; the implementation push is `--force-with-lease` against the approved SHA. Borrow the marker + stale rules for the existing spec-approved label; do not adopt the controller (it is its own pipeline).",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-15"
}
```

**AgentMachinist** -- local-first controller that runs a coding Harness (Claude Code, OpenCode, Goose, …) through **Spec → exact human Approval → Execute (+ verification gates) → read-only Review**, keeping all Git authority in the controller. MIT (`LICENSE` + `pyproject.toml`), Python ≥3.12, PyPI **0.20.0** (uploaded 2026-10-06 15:09 MDT; GitHub release v0.20.0 2026-10-06 14:41 MDT), repo created 2026-08-16, last updated 2026-10-11, ~6★, single author. Releases via PyPI Trusted Publishing with SHA-256 checksums.

Pieces that map onto revvel-standards' `spec-approved` / `wr:code` / `deliver:*` handoff (from the 0.20.0 architecture doc):

- **Immutable approval marker.** Approval evidence is an HTML comment `<!-- agentmachinist:approval sha=<40-hex-head-sha> -->` written by `github-actions[bot]`. The controller only trusts markers authored by the workflow; a marker typed by a human is ignored. Execution needs **both** the label and a marker matching the **current PR head**; label alone = `approval pending`; a branch update = `approval stale`.
- **Actor check before minting.** `/machinist-execute` is only considered from OWNER/MEMBER/COLLABORATOR, and both comment and label paths independently require write/admin. "The permission check fails closed: a permission that cannot be read mints no evidence."
- **A new Spec invalidates Approval**; amendment needs re-approval of the current head.
- **Push safety:** implementation push uses `--force-with-lease` against the approved SHA, so a spec branch changed mid-run fails instead of being overwritten.
- **Verification:** required gates run by the controller are authoritative (Harness self-runs are advisory); file-count/byte/denied-path/binary limits and a refusal to delete test files before commit; optional single bounded repair round.
- **Git metadata custody:** fingerprints `.git` config/hooks/`info/`/alternates before untrusted phases so a planted `core.fsmonitor` or hook cannot run.
- Non-draft PR state outranks a leftover approval label, so a finished PR cannot be re-executed.

**Revvel hit:** the cleanest public description of a label-driven, SHA-bound "spec approved → coder may run" gate. It answers the same question as **agent-approval-check** (merge side) but on the **pre-execute** side: what makes `spec-approved` trustworthy as a trigger for `wr:code`. Borrow: (1) only a bot-minted marker carrying the head SHA counts, never the label alone; (2) permission-read failure = no approval; (3) any push after approval = stale; (4) coder push with lease on the approved SHA. These fit the existing handoff labels (insertion point 4) and `agent-fallback.yml`; no new workflow is implied.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-15 (America/Denver): repo web 200; GitHub API (not archived, Python); release v0.20.0 read; PyPI JSON 0.20.0 (MIT); raw `LICENSE` + `pyproject.toml` read; architecture doc fetched. Tiny (~6★, one maintainer), fast-moving (0.17 → 0.20 in three weeks), and it is a **whole controller**: adopting it would be a second pipeline, which revvel-standards forbids. Pattern-only. Not run on the box.

# boundary-contracts

```json
{
  "id": "boundary-contracts",
  "name": "Boundary Contracts: explicit editable / inspect-only / required / protected artifact roles for coding agents",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.01265"
  ],
  "license": "UNKNOWN (no code released)",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Shape for the spec-approved packet: list each artifact as editable, inspect-only, required or protected before wr:code starts, then gate deliver:* on the diff (torve-style scope globs). Pilot: strictly acceptable patches 9/40 -> 18/40 with the same Codex agent. Paper only; pilot, not general proof.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-03"
}
```

**Toward Bounding Coding-Agent Autonomy in Software Maintenance: A Pilot Study of Boundary Contracts** (Eun, Chung, Park, Lee, Hong, Jung). arXiv **2611.01265** v1, submitted 2026-10-31 15:03 MDT; accepted at JAWS 2 (ASE 2026 workshop). No code link.

A Boundary Contract is a machine-readable record, made before any edit, giving each artifact a role: **editable**, **inspect-only**, **required** (must be touched even if not mentioned) or **protected**. Pilot on 40 maintenance tasks from one enterprise repo, same Codex agent with vs without the contract: macro edit-selection F1 0.440 -> 0.682, required-behavior coverage 0.429 -> 0.673, strictly acceptable patches 9/40 -> 18/40; differences persist on the 21 tasks where both conditions touched a shared file. Authors state the pilot does not establish general effectiveness.

**Revvel hit:** add the four roles to the spec-approved packet (insertion point 3, a shape under `standards/`), and check the coder's diff against them deterministically on an existing job (torve's `scope` gate / spec-growth-engine drift floor already do the glob half). No new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-03 (America/Denver): arXiv export API metadata + abstract (journal comment), abs page 200, HTML version checked for code links (none). Pilot results are the authors'.

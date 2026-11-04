# gated-sdd-audit

```json
{
  "id": "gated-sdd-audit",
  "name": "A Gated Spec-Driven Workflow: audit-trail study of coding-agent work",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.05094",
    "https://github.com/rfa-rodrigo/SDD---Template"
  ],
  "license": "CC-BY-4.0 (template repo)",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Field evidence for the spec-approved -> wr:code -> deliver:* gate shape: a human approval per stage, an executor limited to the files its task declares, and a file-inventory check after every block of tasks. The executor kept to its declared files (1 undeclared change in the deliverable, caught); the weak point was the orchestrator judging its own checks (logged undeclared changes in 11 of 247 block checks, stopped work in only 4). Argues for running the declared-files diff check as a CI step outside the agent (torve scope / boundary-contracts), not as an instruction to the orchestrator.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-04"
}
```

**A Gated Spec-Driven Workflow: An Audit-Trail Study of Coding-Agent Work** (Rodrigo Figueiredo Abdo, Pedro Carvalho Brom). arXiv **2611.05094** v1, submitted 2026-11-03. Workflow template: `rfa-rodrigo/SDD---Template` (CC-BY-4.0 per repo API; six stages pdr -> spec -> plan -> tasks -> execute -> archive, each with a human approval gate; read-only `revisor` subagent, single-writer `executor` subagent; README in Portuguese).

Authors' numbers (nine features, seven projects, all run by the authors, Claude Code): 5 of 9 features finished with every planned task done; 288 of 581 planned tasks completed block by block. The executor left one undeclared change in the deliverable folder and the inventory check caught it. The orchestrator, which runs and judges its own checks, recorded undeclared changes in 11 of 247 block checks and stopped work in only 4.

**Revvel hit:** same shape as revvel-standards' spec-approved packet + wr:code coder. The useful lesson is negative: a check carried out by the model it constrains is skipped or waved through. Put the declared-files / undeclared-change diff in a CI job that fails the PR (torve `scope` gate, boundary-contracts roles, attested receipt), keyed to the file list in the approved spec. No new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-04 (America/Denver): arXiv export API metadata + full abstract; HTML version scanned for code links; template repo API (license, dates) and README read via API. Not run. Results are the authors' own, self-run, small sample.

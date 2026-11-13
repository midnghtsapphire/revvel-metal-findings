# mach2

```json
{
  "id": "mach2",
  "name": "Mach2: rule-gated agent execution with deterministic checks at each lifecycle boundary",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.14777",
    "https://arxiv.org/html/2611.14777v1"
  ],
  "license": "paper arXiv; no code found; paper cites a patent application by the authors (idea only, do not copy implementation)",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Design confirmation for the spec-approved -> wr:code -> deliver:* chain: requirements become executable predicates checked at fixed boundaries (before a tool action: permitted tools and paths; after a code change: AST invariants and TDD outcome; at package build: interface and resource limits; on result import: required fields, task identity, evidence). Mandatory failures block advancement; diagnostics are kept for review. 'An agent's textual declaration of success cannot substitute for a passing rule evaluation.' Results from remote/delegated runs are validated against the declared contract on return, which maps to checking a deliver:* packet from another bot.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-13"
}
```

**Mach2** (arXiv **2611.14777**, Vansh Sharma and Venkat Raman, U. Michigan C-PRIME, submitted 2026-11-10). OpenCode-derived runtime with an orchestrator agent (Eigen), CodeGrapher AST analysis, user-specified TDD and history-guided search. The paper formalizes the rule-gated model and proposes metrics; it does not report a benchmark result.

**Revvel hit:** no new tool. Use it as a checklist to audit whether each existing revvel-standards gate sits at one of the four boundaries and blocks on failure. Overlaps boundary-contracts and gated-sdd-audit.

**Caution:** the authors cite their own patent application for CodeGrapher-style retrieval; treat as idea only.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-13 (America/Denver): arXiv abs page opened (intro, section 2.1, references). No code link seen; no empirical numbers to cite.

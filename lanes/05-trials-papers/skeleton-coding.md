# skeleton-coding

```json
{
  "id": "skeleton-coding",
  "name": "Skeleton Coding: Program Structure as a Specification for Agents",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.38214"
  ],
  "license": "arXiv paper (no code found)",
  "metal": 0,
  "determinism": 3,
  "revvel_hit": "spec-approved could carry a code-like skeleton (types, modules, function signatures) next to the acceptance tests, so the coder fills in a fixed structure instead of choosing one; the paper argues tests alone underdetermine the program.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-30"
}
```

**Skeleton Coding: Program Structure as a Specification for Agents** (Golatkar, Achille, Zabounidis, Sobal, Ding, Ray, Buck, Van den Broeck, Fazel, Perona, Xia, Soatto). arXiv **2610.38214** v1, submitted 2026-10-27 21:09 MDT (cs.SE).

Argument: the number of tests needed to pin down the intended program depends on the structure the agent picks, which the developer cannot see in advance. So the developer specifies the structure too, as a high-level code-like **skeleton** (data types, modules, functions), alongside the behavioural tests. The paper models assisted coding as a control problem and shows skeletons can cut the tests needed exponentially. Authors' numbers across four models and three benchmarks: best skeleton specs cut mean test error 48.4% relative to the best end-to-end behavioural specs; up to 27.0% even when the agent can query a full reference implementation; the small-vs-large model gap narrows about 52.4%; implementation cost drops 15-26x; code erosion drops 24.7%.

**Revvel hit:** a cheap addition to what spec-approved hands wr:code: a skeleton file (signatures and types) plus the acceptance checks, both covered by the approval hash. Fits **spec-guard** / **agent-spec** (structure as part of the approved contract) and **plancompiler** (static checks before emit). Format change inside the existing handoff, not a new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-30 (America/Denver): arXiv abs 200, export API metadata and abstract read. No code or artifact link in the abstract or comment; a GitHub search found none. Results are the authors' own.

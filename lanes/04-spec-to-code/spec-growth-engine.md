# spec-growth-engine

```json
{
  "id": "spec-growth-engine",
  "name": "Spec Growth Engine",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/grabow/spec-growth-engine",
    "https://arxiv.org/abs/2610.11725",
    "https://arxiv.org/abs/2606.27045"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "spec-approved -> wr:code drift floor: one SPEC.md per node with contract, ACs, depends_on and owned code globs; a model-free gate (validate + import-graph drift + lifecycle) blocks a commit whose code imports outside its declared deps, and a node only becomes 'verified' from recorded passing test evidence that a later change voids",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-21"
}
```

**Spec Growth Engine** (Hartwig Grabowski, Hochschule Offenburg). Method paper arXiv 2606.27045; implementation paper arXiv **2610.11725** (submitted 2026-10-08). Code: `grabow/spec-growth-engine`, Apache-2.0, Python 3.12 + `uv`, created 2026-10-08 03:52 MDT, last push 2026-10-10 05:39 MDT, 2★, no release tags.

Two layers kept apart:

- **Layer 1, deterministic floor (no model, no API key):** a graph of `SPEC.md` files (system / container / component), each with a contract (provides, invariants, error behaviour), acceptance criteria, `depends_on`, owned code globs and a status. `cli.py gate` runs **validate** (graph well formed, deps point at nodes with contracts, waivers well formed) and **drift** (builds an import graph from the real code for Python, TS/JS, Java/Kotlin, Dart; an undeclared cross-node import blocks; unowned files and dead globs are reported). **Lifecycle:** `specd -> implemented -> verified`, and `verified` needs recorded, passing test evidence stamped with the run start, voided by a later change. `cli.py install-hook` makes it a git pre-commit hook.
- **Layer 2, agent runs:** intent author, planner, coder (Codex CLI) and a reviewer model grow the graph in rounds; a deterministic rule decides whether the run continues. Delegation is set by three switches (draft gate D0/D1/D2, breaking-change delegation, run mode).

**Revvel hit:** borrow layer 1 only. The "status is earned from recorded test evidence, voided by the next change" rule and the import-graph drift check are exactly what a `spec-approved` -> `wr:code` handoff needs to refuse "done" claims that the code does not back. It overlaps **cadence** (settle gate on ACs) and **attested** (signed test receipts); this one adds the structural drift check against declared dependencies. Do not adopt layer 2: it is a second agent pipeline, which revvel-standards must not grow.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-21 (America/Denver): repo API (Apache-2.0, not fork/archived), README read raw (`gate`, `install-hook`, `check` commands, layer split), arXiv 2610.11725 abs + HTML (200, code link matches). Not run on the box. Two weeks old, one author, 2★, no releases; Python-only engine, and revvel-standards would need its own `SPEC.md` graph before the gate means anything.

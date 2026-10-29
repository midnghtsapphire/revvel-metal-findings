# who-verifies-builder

```json
{
  "id": "who-verifies-builder",
  "name": "Who Verifies the Builder? Independent assurance for agent-produced software",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.28667",
    "https://github.com/besionisrael/assure-harness"
  ],
  "license": "arXiv paper; artifact repo MIT",
  "metal": 0,
  "determinism": 3,
  "revvel_hit": "Shape for the spec-approved -> deliver:* step: a Verification Contract written from the spec before the code exists, checked by a verifier in a fresh context (not the coder's own tests), with the release decision left to a human.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-29"
}
```

**Who Verifies the Builder? Toward Independent Assurance for Agent-Produced Software** (Sion Israel Sion, Alain April; ÉTS Montréal). arXiv **2610.28667** v1, submitted 2026-10-16 12:00 MDT (cs.SE / cs.AI). Artifact: `besionisrael/assure-harness` (MIT, created 2026-10-15, 0 stars).

When one agent writes the code and the tests, a green suite is not independent evidence. The paper separates a **build plane** from an **assurance plane**. A **Verification Contract** states what must be shown before release. Verification runs in two phases: spec-first, without seeing the implementation, then implementation-aware (mutation analysis, property-based testing, fuzzing). The result is an assurance report that leaves the release decision to a human. In a pre-registered study on three stateful services, a verifier in a **fresh context** caught more of 46 seeded faults than the builder's own tests (Holm-corrected p = 0.006) and surfaced spec ambiguities, at the cost of rare false oracles. A verifier from **another provider added no detection** (authors' numbers).

**Revvel hit:** the cheap, borrowable result is "fresh context beats a different vendor". Spec-approved could write the Verification Contract and acceptance checks first, then a fresh-context verifier run checks wr:code output against it before deliver:*. That is a step inside the existing handoff, not a new pipeline. Complements **specguard-lean** (05) and **attested** / **torve** (04).

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-29 (America/Denver): arXiv abs 200, export API metadata, abstract and comment (artifact link) read; artifact repo page 200 and repo API (MIT). Repo contents not inspected. Older than the window (2026-10-16) but not tracked before. Results are the authors' own; nothing run.

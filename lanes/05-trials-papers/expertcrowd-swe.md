# expertcrowd-swe

```json
{
  "id": "expertcrowd-swe",
  "name": "ExpertCrowd-SWE: expert-authored coding tasks with must-pass blockers and control patches",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.13246",
    "https://arxiv.org/html/2611.13246v1",
    "https://huggingface.co/datasets/ExpertCrowd/ec-swe"
  ],
  "license": "dataset card license: other (read before reuse); paper arXiv",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Grader-calibration pattern for the deliver:* gate: every task is calibrated so the reference fix scores 1.0 and both the untouched repo and an inert change score 0, and about half ship lazy and adversarial control patches the grader must classify correctly; must-pass blockers encode what a maintainer would refuse to merge. Copying the 'inert change must score 0' and 'lazy patch must fail' controls into the existing deliver:* checks catches gates that pass empty PRs. Steps per run (33-166 median) had little relation to score (authors).",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-12"
}
```

**ExpertCrowd-SWE (EC-SWE)** (arXiv **2611.13246** v1, submitted 2026-11-09). 100 multi-file change requests by practising engineers against pinned commits in 87 projects / 11 languages, each with a sealed reference solution and a weighted, mostly executable grader. 3,495 scored runs across seven frontier models; top two 67.3% and 63.7% (no significant gap). 24 tasks with environments, graders and results released on Hugging Face (`ExpertCrowd/ec-swe`), 76 held out. HTML cites `hud-evals/hud-python` and `SWE-agent/mini-swe-agent` as harness pieces.

**Revvel hit:** add two control cases to the existing deliver:* gate's tests: an inert change and a lazy patch, both must fail. That proves the gate rejects do-nothing PRs. Fits beside continuous-benchmarks and gated-sdd-audit; no new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-12 (America/Denver): arXiv export API abstract; HTML v1 opened (dataset link); Hugging Face dataset API (public, not gated, license `other`). Dataset not downloaded; numbers are the authors'.

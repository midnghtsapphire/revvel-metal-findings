# reprobridge

```json
{
  "id": "reprobridge",
  "name": "ReproBridge: Building Reproducibility into ML Research Artifacts",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.08452",
    "https://arxiv.org/html/2611.08452"
  ],
  "license": "n/a (paper; no public code URL found on abs/HTML)",
  "metal": 1,
  "determinism": 3,
  "revvel_hit": "Standardized refined artifact packet (codebase + environment + launchers + reproduction guide) raised mean reproduction success 76.4% -> 92.6% and cut downstream API spend 19.7% across four models; cross-model spread narrowed 21.6 -> 3.9 pp (authors, ReproBridge-Bench 1,029 tasks). Evidence for the deliver:* artifact shape: ship recovered procedures with the packet, not raw code alone. Do not adopt the ReproBridge agent workflow as a second pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-06"
}
```

**ReproBridge** (Wang, Meng, Nam, Pfister, Yoon). arXiv **2611.08452** v1, submitted 2026-11-05. Defines a refined reproducible artifact (codebase, environment setup, experiment launchers, reproduction guide) and an agent workflow that builds it. **ReproBridge-Bench**: 1,029 tasks from 387 experiments across 36 papers, five human-verified reference scores per task. Across four models, refined artifacts raise mean reproduction success from **76.4% to 92.6%** and reduce downstream API spending by **19.7%** on average; cross-model success-rate spread narrows from **21.6 to 3.9** percentage points (authors). Ablations: removing any component hurts; largest losses from code and environment removal.

**Revvel hit:** shape evidence for the deliver:* packet — preserve recovered procedures and decisions with the code, environment, and launchers. Auditor-checks-execution-evidence is the same idea as cadence / attested. Watch for a code release; do not stand up ReproBridge as a parallel agent OS.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-06 (America/Denver): arXiv export API abstract; arXiv abs and HTML opened; no GitHub / Zenodo / Hugging Face artifact URL found in the HTML. Not run. Numbers are the authors'.

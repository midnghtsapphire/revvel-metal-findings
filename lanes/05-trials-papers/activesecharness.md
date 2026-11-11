# activesecharness

```json
{
  "id": "activesecharness",
  "name": "ActiveSecHarness: Compositional Security for Agentic Coding Harnesses",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.13960",
    "https://arxiv.org/html/2611.13960v1"
  ],
  "license": "n/a (paper; no code URL on abs/HTML)",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Deterministic Ring-0 OS/tool guards blocked all 120 attack fixtures with 0 false positives in 12.7 microseconds, while a local LLM judge (qwen3:4b) refused 98.3% of benign work at 142 ms (authors, N=252). A 2D trust x sensitivity taint lattice plus a workspace provenance ledger caught all 12 kill chains where a stateless policy missed 4. Supports keeping the deliver:* coder's guard deterministic in the existing mcp-gate / mcp-hangar / verax path, never an LLM judge.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-11"
}
```

**ActiveSecHarness** (arXiv **2611.13960** v1, submitted 2026-11-10). Neurosymbolic reference monitor built on separating intelligence from authority: HMAC capability tokens (Macaroon-style) across four trust rings, a product taint lattice (trust x sensitivity) with a workspace provenance ledger to stop secret laundering through disk, deterministic Ring-0 guards, bytecode certificates and split-horizon audit logs. Results (authors): Ring 0 ABR 1.000 / FPR 0.000 at 12.7 us (11,200x faster than the LLM judge); 2D lattice ABR 1.000 / FPR 0.000 at about 20 us per step on multi-step trajectories; coarse Boolean taint blocks 83.3% of benign workflows.

**Revvel hit:** borrow two rules for the existing deliver:* gate: (1) capability tokens scoped per WR instead of ambient credentials, and (2) taint that tracks both trust and sensitivity, so a file written from untrusted retrieved content can't later be pushed with a secret. Fits beside germline-exec and delegated-scope. No new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-11 (America/Denver): arXiv export API abstract; HTML v1 opened, no code link. Not run. Numbers are the authors'.

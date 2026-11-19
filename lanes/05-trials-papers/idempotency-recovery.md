# idempotency-recovery

```json
{
  "id": "idempotency-recovery",
  "name": "Idempotency Is Not Recovery + Checking Retry Transparency: interrupted agent tool calls need a ledger and reconciliation, not just retry",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2611.23353",
    "https://arxiv.org/abs/2611.23307"
  ],
  "license": "papers arXiv; no code link on abstract pages",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "For deliver:* side effects (label apply, PR open, merge, release): an interrupted call must be reconciled against the target (does the PR/label exist?) before any retry. Full runtime with action ledger + target-side idempotency + reconciliation repeated 0/200 effects vs 117/200 for simpler baselines; without reconciliation 100/100 post-effect crashes stayed ambiguous. Retry-transparency paper: blind retry completed 9 of 27 missing-reply checks with 3 goal violations.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-19"
}
```

**Idempotency Is Not Recovery: A Fault-Injection Study of Language-Model Agent Tool Actions** (arXiv **2611.23353**, 2026-11-17): ten fault classes, 7,513 trials each on Windows and Linux. Full config 0/200 repeated effects vs 117/200 per simpler baseline; ledger ablation 170/170 orphaned effects; recovery 300/300 vs 200/300. Cost: about one-seventh of fail-open throughput; evidence-write faults left 75/100 trials per platform unresolved.

**Checking Retry Transparency in Agent Tools** (arXiv **2611.23307**, 2026-11-11): source-backed effect contracts checked as retry-absorption obligations and bounded interleavings over 6 MCP components; selective rule completed 6 justified workflows with no acknowledged violation, strict coalescing 0, blind retry 9 with 3 violations; Porcupine spec agreed with all 156 oracles.

**Revvel hit:** in the existing deliver:* job (no new pipeline): write an intent line (WR id, action, target) before each GitHub side effect, and on restart look up the target first (PR by head branch, label present, merge SHA) instead of re-running. Cheap, deterministic, and avoids duplicate PRs/labels from retried runs.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-19 (America/Denver): both arXiv abs pages opened. No code seen; numbers are the authors'.

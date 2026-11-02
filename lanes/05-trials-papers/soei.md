# soei

```json
{
  "id": "soei",
  "name": "Soei: structured observability of evidence and intent for coding agents",
  "lane": "05-trials-papers",
  "status": "watching",
  "urls": [
    "https://arxiv.org/abs/2610.39468"
  ],
  "license": "arXiv paper (no code found)",
  "metal": 1,
  "determinism": 4,
  "revvel_hit": "Field numbers for why deliver:* must separate a completion claim from proof: on 45 real coding-agent sessions, 23.4% of code-editing episodes ended with no independent check after the last edit and 57.8% of to-dos marked complete after editing had no proof in between. Supports cadence / attested / pcm; proposes a hash-chained local ledger that replays deterministically. Paper only.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-02"
}
```

**Soei: Structured Observability of Evidence and Intent for Multi-Agent AI Software Engineering** (Mohammed Nayeem Khan, K S Sarun Kumar). arXiv **2610.39468** v1, submitted 2026-10-29 00:40 MDT (cs.SE).

Three parts. (1) An audit of the open-source Agenttrail observability tool against its source at commit `e4ba2da` (nine documented mechanisms hold; two event pipelines never unified; an unauthenticated local mutation surface). (2) A prototype run on **45 real coding-agent sessions** (102,233 records, 20,577 tool executions, 2,336 human-to-agent episodes): with a blind-audited classifier (precision 83.3% and 96.7%) the authors estimate **23.4%** (95% CI 17.1-35.7) of code-editing episodes end with no independent check after the last edit, and **57.8%** of to-dos the agent marked complete after editing had no proof in between; 42% of sessions run > 24 h; 1,326 records in 16 sessions contain credential-like strings. (3) The Soei proposal: acknowledgement-aware event schema, **hash-chained local ledger**, W3C PROV-aligned graph, and a verification layer that keeps a claim of completion apart from proof; on the same corpus the ledger is 20% of raw size, holds no content or credentials, verifies at ~126k events/s, detects tampering and replays deterministically.

**Revvel hit:** measured evidence for the rule cadence, attested and pcm already encode: the coder saying "done" is a claim; deliver:* should accept only a check that ran after the last edit. Borrow the metric itself ("was there an independent check after the last edit?") as a cheap deliver:* gate input. No new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-02 (America/Denver): arXiv abs 200, export API metadata and abstract read. No code link found in the abstract or PDF. Numbers are the authors' own, one corpus of 45 sessions.

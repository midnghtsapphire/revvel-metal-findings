# concordance

```json
{
  "id": "concordance",
  "name": "CTGT Concordance",
  "lane": "01-deterministic-ai",
  "status": "watching",
  "urls": [
    "https://github.com/CTGT-Inc/concordance",
    "https://www.ctgt.ai/research/concordance"
  ],
  "license": "Apache-2.0",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "pipeline-level determinism check: a deterministic model still gives different wr:code results when the pipeline writes per-run values (ids, unordered lists, growing registries) into prompts; stdlib-only compare_runs.py groups identical requests across runs and names the first stage that diverged",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-22"
}
```

**Concordance** -- CTGT's measurement and reproduction package, released 2026-10-21 (repo created 2026-10-20 23:53 MDT, last push 2026-10-21 00:08 MDT, 11★, Apache-2.0). Write-up "Deterministic Inference Did Not Make Our Pipeline Deterministic" (2026-10-21).

Finding: Qwen3.8-27B on SGLang with `--enable-deterministic-inference` matched a batch-size-1 control in 800 of 800 replies, yet four runs of one document through their ingestion pipeline committed four different results (32, 31, 33, 33 obligations; one run dropped an escalation rule). Every changed answer followed a changed request: the pipeline put a hash of a per-upload UUID, an unordered 30-item list, and a registry that grew between runs into its prompts. After aliasing the ids, sorting the list and pinning the registry, five runs committed the same result. Their own caveat: "Stable is not correct" -- a wrong classification also replayed 8 of 8 times.

Parts: `compare_calls/compare_runs.py` (stdlib only; given captured model calls from two or more runs of any pipeline, groups identical requests, reports whether outputs changed, finds near-identical requests and the differing lines, and names the first diverging stage), `toy_pipeline/` (three-stage repro against any OpenAI-compatible endpoint), `inference/` (benchmark + SGLang launch), `data/` (stage hashes only, no prompts). The production engine is not included.

**Revvel hit:** this is the missing check next to **vllm-batch-invariance** / **deepinfer** / **vosti**: those make the model repeatable, this shows whether the wr:code / deliver:* prompt builder is. Rule to adopt now, no tool needed: nothing per-run (UUIDs, timestamps, set/dict iteration order, a growing label or file registry) goes into a coder prompt; sort and alias it first. If two wr:code runs on the same WR diverge, capture the calls and run `compare_runs.py` before blaming the model. It reads captures, so it adds no second pipeline. Pair with **agentverify** 0.7.0's stale-cassette prompt diff.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-22 (America/Denver): repo API (Apache-2.0, not fork/archived), README read raw, write-up page 200 and read. Numbers are the vendor's own, one model, one pipeline; one day old, no releases. Not run on the box.

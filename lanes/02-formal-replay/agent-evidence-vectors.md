# agent-evidence-vectors

```json
{
  "id": "agent-evidence-vectors",
  "name": "Agent Evidence Vectors (probityai/agent-evidence-vectors)",
  "lane": "02-formal-replay",
  "status": "watching",
  "urls": [
    "https://github.com/probityai/agent-evidence-vectors",
    "https://github.com/probityai/agent-evidence-vectors/releases/tag/v0.20.0",
    "https://pypi.org/project/agent-evidence-vectors/",
    "https://github.com/probityai/agent-evidence-vectors/tree/v0.20.0/vectors-a2a-jcs-v01",
    "https://github.com/probityai/agent-evidence-vectors/releases/tag/v0.24.0"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "Known-answer test vectors for whatever verifies deliver:* approval/receipt bytes: score the canonicalizer behind the approval digest (agt-approval-protocol pattern) against the a2a-jcs RFC 8785 corpus (`A2A_JCS_TARGET: rfc8785`), and receipt/ledger verifiers (mcp-gate, agent-gate, verax) against the tamper corpora. Runs as `uvx agent-evidence-vectors==0.20.0 --verifier <cmd>`; a CI step on an existing job would need owner OK. Reference only until revvel-standards writes its approval-record schema",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-19",
  "updated": "2026-10-20"
}
```

**Agent Evidence Vectors** -- conformance corpora plus reference verifiers (Python harness, Go `aee-verify`) for AI-agent and supply-chain evidence formats. Each vector is a saved record with a known outcome: valid, altered bytes, missing evidence, or an open spec interpretation. Your verifier is called with a vector path and returns its verdict via exit status + a JSON line; the harness writes `conformance-report.json` and separates conformance from reason-code agreement. A composite **GitHub Action** (`action.yml`) runs the same check in CI; a `vectors:` input can point at a corpus directory pinned by your own workflow, and the report carries that corpus's recomputed digest.

Shipped corpora at v0.20.0 include `vectors-a2a-jcs-v01` (the a2a-tck Agent Card canonicalization corpus; `A2A_JCS_TARGET: rfc8785` scores a bare RFC 8785 canonicalizer), `vectors-receipt-chain-end`, `vectors-receipt-signature`, `vectors-anchored-chain`, `vectors-done-contract`, `vectors-done-receipt`, `vectors-agent-change-admission`, `vectors-authority-at-dispatch`, `vectors-test-tampering`, `vectors-spoofed-tool-output`, `vectors-mcp-record-contract`, and more. Default corpus at v0.20.0 is suiteRevision 32: README shows `288 vectors, 288 pass` for the bundled reference verifier.

**v0.20.0:** GitHub release 2026-10-18 16:13 MDT (PyPI upload 2026-10-18 02:32 MDT); signed corpus digest list with RFC 3161 and OpenTimestamps proofs; adds an invocation-axes reader (one pinned MCP `tools/call` judged on package integrity, request/decision correspondence, observed effect), done-run predicates, delegation-lifecycle recovery cases; the verifier now checks the run-end seal signature in every case. 18 PyPI releases since 0.11.1 (2026-09-16). Repo Apache-2.0, created 2026-07-21, last push 2026-10-18 20:53 MDT, 6★, single maintainer.

**Revvel hit:** revvel-standards' deliver:* consent story is converging on "approve a digest of exact bytes" (**spec-guard**, **agent-approval-check** SHA binding, **hashgate** / **notary-mcp** patterns, **agt-approval-protocol** record). AGT's own digest was wrong on RFC 8785 number formatting until #4341 (2026-10-16), and these vectors are what caught it. If revvel writes its own canonicalizer or receipt verifier, this is a ready known-answer suite instead of hand-made fixtures. It plugs into the existing workflows as one step; no new pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-19 (America/Denver): GitHub repo + release API (Apache-2.0, not archived; v0.20.0 body read), PyPI JSON (0.20.0, Apache-2.0), README and `action.yml` read raw at `main` / `v0.20.0`, repo + release + corpus tree pages 200. Not run on the box. Young, single-maintainer project with a broad scope; only the canonicalization and receipt corpora are in scope. Adding its Action to revvel-standards would be a workflow edit, so it needs Audrey's OK.

**Update 2026-10-20 -- v0.21.0 → v0.24.0 in one day** (GitHub releases 2026-10-19 12:13, 13:25, 16:54, 20:12 MDT; PyPI 0.24.0 uploaded 20:05 MDT; still Apache-2.0). Every release states that **no case shipped earlier changes verdict**; v0.21.0 states every v0.20.0 case is byte-identical except the `invocation-axes` binding_rule text, so the a2a-jcs RFC 8785 cases are unchanged. Additions in scope for revvel: **v0.21.0** adds a call binding (`callBinding`) and a new **occurrence-binding** corpus (16 cases: an execution or payment receipt must name the exact call occurrence, not just identical call content -- e.g. `same_content_different_execution`, `execution_names_call_content_only`), an `observed-invocation-binding` candidate profile (25 fixtures, incl. `params-value-changed-mismatch`, `unsigned-binding-change`), and two new `invocation-axes` cases; `binding_rule` now excludes `params._meta`. **v0.22.0** adds `vectors-chunked-export` (12 cases; rules partly marked Proposed). **v0.23.0 / v0.24.0** add delegation-lifecycle succession and sub-agent cases (5 + 7 cases; one v0.23.0 case and every v0.24.0 sub-agent rule marked Proposed) and 10 more occurrence-binding cases (lost call, input pin). Out of scope: payment/budget and delegation corpora.

**Revvel hit (2026-10-20):** the occurrence-binding cases are the known-answer test for "an approval is consumed by exactly one execution": if the deliver:* approval record (agt-approval-protocol pattern) is ever written, test that a receipt naming only the call content, or a different occurrence, is rejected. Pin an exact version (`agent-evidence-vectors==0.24.0`) because each minor adds cases a verifier may not pass. Still watching; a CI step still needs Audrey's OK.

**Honesty (2026-10-20):** CAN-PARTIAL. Verified 2026-10-20 (America/Denver): GitHub release bodies v0.21.0–v0.24.0 read (API), release page v0.24.0 200, PyPI JSON 0.24.0 (Apache-2.0). Not run on the box. Release cadence is very fast (four minors in ~8 hours) for a single-maintainer project.

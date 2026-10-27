# agent-evidence-vectors

```json
{
  "id": "agent-evidence-vectors",
  "name": "Agent Evidence Vectors (probityai/agent-evidence-vectors)",
  "lane": "02-formal-replay",
  "status": "watching",
  "urls": [
    "https://github.com/probityai/agent-evidence-vectors/releases/tag/v0.28.0",
    "https://github.com/probityai/agent-evidence-vectors/releases/tag/v0.26.0",
    "https://github.com/probityai/agent-evidence-vectors",
    "https://github.com/probityai/agent-evidence-vectors/releases/tag/v0.20.0",
    "https://pypi.org/project/agent-evidence-vectors/",
    "https://github.com/probityai/agent-evidence-vectors/tree/v0.20.0/vectors-a2a-jcs-v01",
    "https://github.com/probityai/agent-evidence-vectors/releases/tag/v0.24.0"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "Known-answer test vectors for whatever verifies deliver:* approval/receipt bytes. Since v0.26.0 a dedicated approval-binding corpus (approval-binding/v1, 23 cases: already-consumed, payload-mutated-after-approval, asserted-in-tool-arguments, used-at-expiry, target/tool/phase differs) is the KAT set for the spec-approved / deliver:* approval check. Runs as `uvx agent-evidence-vectors==<pin> --verifier <cmd>`; a CI step on an existing job needs owner OK. Keep ==0.24.0 for the canonicalization/occurrence-binding corpora; use ==0.26.1 only for approval-binding after a diff (its corpus files are identical at v0.28.0). v0.27.0/v0.28.0 add dispatch-fence, converted-argument-binding, authority-at-dispatch and proof-of-control corpora (KATs for 'the deliver:* call that ran is the one approved'); use ==0.28.0 only for those, after a diff. Reference only until revvel-standards writes its approval-record schema",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-19",
  "updated": "2026-10-27"
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

**Update 2026-10-22 -- v0.25.0** (GitHub release 2026-10-21 18:35 MDT; PyPI 17:07 MDT; Apache-2.0). **First release since v0.20.0 that changes existing cases:** five corpora move to suite revision v2 and some cases are renamed, removed or rewritten, so a consumer pinned to earlier case names must re-pin. `vectors-done-receipt` goes done-receipt/v1 to v2 (196 to 227 cases; 84 new, e.g. `forged-receipt`, `completion-claim-dropped`, `integrity-laundered`, `grade-pinned-to-other-bytes`); reads observation v3 and receipt v2; adds a done-probes corpus and ten observed-effect cases that locate a coverage gap in time; derives `effect_under_authority` in the invocation axes. The release notes do not say whether the a2a-jcs RFC 8785 or occurrence-binding cases changed.

**Revvel hit (2026-10-22):** the done-receipt cases (forged receipt, dropped completion claim, grade pinned to other bytes) are the known answers for any "deliver:* is done" receipt, the same job **attested** and **cadence** do. Keep the pin at `==0.24.0` until someone diffs the canonicalization and occurrence-binding corpora at v0.25.0; a CI step still needs Audrey's OK.

**Honesty (2026-10-22):** CAN-PARTIAL. Verified 2026-10-22 (America/Denver): GitHub releases API body for v0.25.0 (first ~1.8k chars), PyPI JSON 0.25.0. Corpora not diffed.

**Update 2026-10-26 -- v0.26.0 and v0.26.1.** **v0.26.0** (GitHub release 2026-10-25 22:10 MDT; PyPI 0.26.0 uploaded 2026-10-25 19:56 MDT; Apache-2.0). Minor release; per its notes:

- **New `vectors-approval-binding` corpus** (approval-binding/v1, 23 cases), e.g. `allow-bound`, `allow-same-approval-presented-twice`, `approval-already-consumed`, `approval-asserted-in-tool-arguments`, `approval-id-reused-different-content`, `approval-key-not-approvers`, `payload-mutated-after-approval`, `target-differs`, `tool-differs`, `phase-differs`, `used-at-expiry`, `used-before-issued`, `release-retired-beyond-grace`.
- `vectors-agent-audit-record` 71 -> 111 cases (tests `draft-gilda-audit-agent-audit-record-00`); **69 of the 70 kept cases carry rewritten records (file IDs moved; re-pin from `ID-MAP.json`)** and `n1-anchor-token-with-no-offline-rule` is removed. No kept case changes its expected result.
- +1 acs-core, +2 anchor-stream, +2 source-coverage cases; three new packaged corpora (operand provenance 13, evaluation result readings 19, evaluation claim record 60).
- Signed corpus digest list with RFC 3161 and OpenTimestamps proofs.

**v0.26.1** (tag `v0.26.1`, no release body; PyPI 2026-10-26 08:28 MDT): per the v0.26.0...v0.26.1 compare, adds a "recorded" corpus class (bytes recorded from live runs), a stdlib-only corpus digest, and re-signed digests. After it, `main` gained an unreleased "dispatch-fence and argument-binding corpora" commit (#253, 2026-10-26 07:55 MDT) -- watch for it in the next release.

**Revvel hit (2026-10-26):** approval-binding is the first corpus aimed squarely at the spec-approved gate: an approval that is reused, consumed twice, applied to a mutated payload, smuggled in tool arguments, or used at/after expiry must be refused. If revvel-standards ever writes the deliver:* approval record, run this corpus against its checker. Keep `==0.24.0` for existing corpora; take `==0.26.1` only for approval-binding, after diffing the canonicalization and occurrence-binding cases. A CI step still needs Audrey's OK.

**Honesty (2026-10-26):** CAN-PARTIAL. Verified 2026-10-26 (America/Denver): GitHub releases API body v0.26.0 read, PyPI JSON 0.26.0/0.26.1 upload times, compare API v0.26.0...v0.26.1 (CHANGELOG at the v0.26.1 tag returned 404), commits API for #253. Corpora not run or diffed.

**Update 2026-10-27 -- 0.26.2 → 0.27.0 → 0.28.0.** PyPI: 0.26.2 (2026-10-26 13:46 MDT), 0.27.0 (2026-10-26 23:30 MDT), 0.28.0 (2026-10-27 08:06 MDT); GitHub release only for **v0.28.0** (2026-10-27 08:36 MDT); v0.26.2 and v0.27.0 are tags without release pages.

- **v0.27.0** ships the corpora the 10-26 scrape was hunting: new top-level `vectors-dispatch-fence`, `vectors-converted-argument-binding` and `vectors-poc-evidence` (Proof-of-Control, 171 cases, #259), from #253 (dispatch-fence / argument-binding); package adds `dispatchfence.py` / `authoritydispatch.py`. `vectors-authority-at-dispatch` is present at v0.28.0.
- **v0.28.0** adds a `vectors-trade-booking` corpus and command, grows agent-audit-record to 141 members (59 accept / 81 reject / 1 indeterminate; adds A21, SQ1–SQ5, R10–R16), binds consumption state with an operation key, and regenerates digests/stamps.
- The **approval-binding corpus files are byte-identical between v0.26.1 and v0.28.0** (tree compare).

**Revvel hit (2026-10-27):** dispatch-fence / argument-binding are the KATs for the second half of the spec-approved gate: the call that actually dispatches must carry the arguments that were approved, with authority checked at dispatch, not at approval time. Pins: keep **==0.24.0** for existing corpora; **==0.26.1** stays fine for approval-binding; take **==0.28.0** only for the dispatch-fence / argument-binding corpora, after a diff. Any CI step still needs owner OK. Reference only until revvel-standards writes its approval-record schema.

**Honesty (2026-10-27):** CAN-PARTIAL. Verified 2026-10-27 (America/Denver): PyPI JSON upload times, GitHub releases API (v0.28.0 body read), git trees API for v0.26.1 / v0.27.0 / v0.28.0 (top-level corpora and approval-binding blob SHAs compared). Corpora not run.

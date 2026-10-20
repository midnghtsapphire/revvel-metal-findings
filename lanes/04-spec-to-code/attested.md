# attested

```json
{
  "id": "attested",
  "name": "attested (Praxso/attested)",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/Praxso/attested",
    "https://github.com/Praxso/attested/blob/main/docs/ruleset.md",
    "https://github.com/Praxso/attested/blob/main/action.yml",
    "https://www.npmjs.com/package/@praxso/attested"
  ],
  "license": "Apache-2.0",
  "metal": 1,
  "determinism": 5,
  "revvel_hit": "deliver:* merge side, evidence half: the coder's PR must carry a Sigstore-signed (actions/attest) in-toto receipt of the repo's own test run bound to the PR head SHA, checked by a required `attested verify` status that runs from the default branch and never runs PR code; fails closed on no receipt / wrong signer workflow / SHA mismatch / FAILED. Sits beside agent-approval-check (human approvals) on the same required-checks list. Pattern first; adopting it is a workflow edit (point 5 job + ruleset), so it needs owner OK. No second pipeline",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-20"
}
```

**attested** -- signed, verifiable test receipts for agent-authored pull requests (Apache-2.0). `attested run -- <test command>` wraps any test run that writes a [CTRF](https://ctrf.io) report (README quickstart is Playwright) and builds an **in-toto Statement** whose subject is the CTRF report and whose predicate (`https://praxso.ai/attested/v0.1`) records the result, failing tests, `source.commit` / `source.headCommit`, and the sha256 of every trace, video, and screenshot. `run` refuses a dirty tree and refuses to start when `HEAD` differs from `--expect-sha`. In GitHub Actions a separate **sign** job (`id-token: write`, `attestations: write`) runs only attested from the base commit, rebuilds the receipt from the downloaded results (`attest --from-results`, every file treated as data, digests recomputed), and signs it with Sigstore keyless signing via `actions/attest`.

The **`attested verify`** composite action (`action.yml`) fails closed, one line per rule: `no receipt`, `no attestation found`, `predicate type mismatch`, `verification failed` (`gh attestation verify` with `--signer-workflow`), `no attestation from run <id> on <ref>` (certificate must name the exact run and `refs/pull/<N>/merge` or `refs/heads/main`), `SHA mismatch` (head rule), `result FAILED` / `missing` / `unknown`, `test command failed`, `unsigned run from fork`. Hardened form: an organization ruleset requires the verify **workflow** by identity; the minimal form (`docs/ruleset.md`) is a repository ruleset requiring the check name `attested verify`, which the docs call weaker. A PR that edits the attesting or verify workflow is blocked pending admin bypass. Also ships a stdio MCP server (`@praxso/attested-mcp`: `attested_run`, `attested_packet`, `attested_status`) and a Claude Code / Codex skill telling the agent to run tests through attested instead of posting screenshots; on red it writes a redacted failure packet (≤ 12 KB, tokens/emails masked).

**Releases:** npm `@praxso/attested` and `@praxso/attested-mcp` **0.1.0** (published 2026-10-15 18:39 MDT; Apache-2.0 in registry metadata). No GitHub releases. Repo created 2026-10-14 14:58 MDT, last push 2026-10-20 06:56 MDT (tip `5e972b3772401150ffb00cb5bc569ecd4459bbc5`), 0★, single org; README status "M2".

**Revvel hit:** revvel-standards' deliver:* merge side today has a human-approval gate candidate (**agent-approval-check**) but nothing that proves the coder's tests actually ran green on the exact head SHA; a green check from a job the PR itself can edit is weak. attested's split (tests run with a read-only token; signing and verification run from the base branch; receipt bound to head SHA by a Sigstore certificate naming the run) is the evidence half of that gate. It reuses GitHub's own attestation store, so no hosted service. Insertion: one `attested run` + `sign` + `verify` on an existing job in the coder/spine workflow (point 5) plus a ruleset entry for `attested verify` -- an edit to revvel-standards workflows and rulesets, so it needs Audrey's OK. revvel-standards is a user-owned repo, so only the weaker repository-ruleset form applies. Pairs with **gh-actions-lock** (pin `Praxso/attested@<full sha>` and `actions/attest`) and with **agent-evidence-vectors** (receipt-verifier conformance) if ever adopted.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-10-20 (America/Denver): GitHub repo API (Apache-2.0, not a fork, not archived), README, `docs/ruleset.md` and LICENSE read raw at `main`; repo, `docs/ruleset.md`, `action.yml`, `SECURITY.md` pages 200; npm registry JSON for both packages (0.1.0; npmjs.com web page 403s the fetcher, as for other npm entries). Not run on the box. Six days old, 0★, single maintainer org, pre-1.0 predicate type (`v0.1`). A receipt proves the PR's own test suite reported a result, not that the change is correct: the README says a PR can still weaken or delete its own tests (a "tests disappeared vs base receipt" check is only planned). Anyone with admin rights, including an agent on an admin account, can bypass rulesets.

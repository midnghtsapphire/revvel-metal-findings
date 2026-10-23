# gh-actions-lock

```json
{
  "id": "gh-actions-lock",
  "name": "GitHub Actions workflow lockfiles (gh actions-lock)",
  "lane": "02-formal-replay",
  "status": "active",
  "urls": [
    "https://github.com/github/gh-actions-lock",
    "https://github.com/github/gh-actions-lock/releases/tag/v0.2.0",
    "https://github.com/github/gh-actions-lock/releases/tag/v0.3.0",
    "https://github.blog/changelog/2026-10-14-github-actions-workflow-lockfiles-in-public-preview/",
    "https://github.com/github/gh-actions-lock/pull/186"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Pin every `uses:` in the existing wr:code / deliver:* workflows (openrouter-coder.yml, revvel-engine-spine.yml, agent-fallback.yml, trusted-bot-auto-approve.yml) to reviewed commits via `.github/workflows/actions.lock`; GitHub then runs the locked commits even if a tag or branch moves. `gh actions-lock --verify` as a step on an existing job fails the run on drift. Same workflows, no second pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-16",
  "updated": "2026-10-23"
}
```

**gh-actions-lock** -- GitHub's own `gh` CLI extension for workflow dependency lockfiles, part of its Workflow Dependency Pinning effort. `gh actions-lock` scans `.github/workflows/`, resolves each action (and transitive and reusable-workflow dependencies) to a commit SHA, and writes `.github/workflows/actions.lock`. Once a workflow is onboarded, GitHub Actions requires a lockfile entry for each of its dependencies and runs the recorded commit, even if the tag or branch moves later. Locked pins are sticky and re-checked the way the runner checks them at job start (repo not renamed/transferred, commit still exists, full-version tags still point at it); a failed check blocks the run. Writes are all-or-nothing. `--verify` is the CI check (fails on unused entries and on workflows without entries since v0.2.0); `--verify-local` is offline and never writes; `--relock` re-resolves legitimately moved refs; `--accept-moved` is needed for pins whose commit vanished upstream. Same-repo actions can use `uses: $/…`, which resolves to the running commit and needs no entry (fix runs rewrite `./…` composite refs to `$/…` unless `--no-migrate-local-actions`). A **Require lockfile** policy (public preview) can be set at repo/org/enterprise level, and Dependabot regenerates the lock entry in its own action-update PRs.

v0.2.0 (2026-10-12 13:31 MDT): lockfile schema `v0.0.3`, stricter `--verify`, `--rescan` removed (runs are sticky), rejects expressions in `uses:`, warns on mutable Docker image tags, cooldown honours the Dependabot config. Repo: MIT, created 2026-04-21, last push 2026-10-15 08:42 MDT, ~218 stars.

**Revvel hit:** the deliver:* handoff is only as deterministic as the Actions code it runs. Today a moved `@v4` tag on any action in the coder/spine workflows changes what runs with no diff in revvel-standards. Locking them makes a wr:code run reproducible from the repo SHA alone, and pairs with **agent-approval-check**'s "pin action SHA" note and the replay lane (**chronicle** / **agentape** replay the model; the lockfile pins the runner side). Insertion: commit `actions.lock` + any `$/` rewrites to the existing workflows and add `gh actions-lock --verify` as a step on an existing job (point 5). It touches revvel-standards workflow files, so it needs Audrey's OK before anyone opens that PR.

**Honesty:** CAN-PARTIAL. Verified 2026-10-16 (America/Denver): repo and v0.2.0 release via GitHub API (not a prerelease); README read in full; changelog page 200 and read. The changelog's editor's note (2026-10-14) says the preview covers GitHub Enterprise Cloud, GHE.com data residency, **Team, and Free** plans; GHES is not supported. Pre-1.0 public preview: the README warns the lockfile format, flags, and behaviour may change between releases (schema already moved to v0.0.3). The `$/` syntax is new runner behaviour, so check that every workflow still runs after migration. Locking does not vet the pinned code itself. Not trialled on revvel-standards.

**Update 2026-10-20 -- install-source warning + unreleased fix:**

- **Look-alike repos.** GitHub search on 2026-10-20 returns **33 non-fork repos named exactly `gh-actions-lock`** under unrelated personal accounts, created 2026-10-14 → 2026-10-20, all with an unrecognised license (`NOASSERTION`) and the official description copied verbatim. The ones checked carry the copied README, fabricated-looking commit histories and implausible release tags (e.g. `v3.272.503`). Not downloaded or run; treat them as untrusted. A `gh extension install <owner>/gh-actions-lock` from any of them would run their binary. **Only install `github/gh-actions-lock`**, and pin the extension (`gh extension install github/gh-actions-lock --pin <tag or sha>`) in any CI step. Separately, `navikt/gh-actions-lockfile` (created 2026-10-19, no license) is an org-wide onboarding web app that wraps the official tool; not relevant to a single repo.
- **Unreleased on `main`:** "Trace every locked commit to its recorded ref" (#186, merged 2026-10-20 07:03 MDT, closes #174): every locked commit is checked, in every mode, against the history of its recorded tag or branch (looked up by exact name, as the Actions backend does), so **a fork-only commit can no longer pass under the upstream action's name**; a recorded ref rewritten or deleted so it no longer contains the commit, a ref that isn't a real tag/branch, and a malformed `uses:` now **block** instead of passing silently; an exact tag that only moved ahead warns under `--verify`. Follow-up fixes for v0.2.0 bugs are in #197. Latest release still **v0.2.0**; wait for the release before relying on it.

**Honesty (2026-10-20):** verified 2026-10-20 (America/Denver): GitHub repo-search API (count and metadata), repo / releases / commits API for sample look-alikes, READMEs viewed (not cloned, nothing executed); `github/gh-actions-lock` commits API, PR #186 API (body read) and page 200; releases API (v0.2.0 still latest). Malicious intent is inferred from the pattern, not confirmed by inspecting binaries.

**Update 2026-10-23 -- v0.3.0 released (breaking for `--verify`):** published 2026-10-22 10:08 MDT. Lockfile schema unchanged (`v0.0.3`), but some lockfiles that passed `--verify` on v0.2.0 now fail it:

- **#186 shipped** (the impostor-commit fix tracked here since 10-20): every locked commit must be in the history of its recorded tag or branch, so a fork-only commit can't pass under the upstream action's name; refs like `main~1` or `git describe` output are rejected.
- An exact tag locked behind its commit is now a `tag-commit-mismatch` error; older lockfiles can fail with `incomplete-lockfile`. Both fix with `gh actions-lock --relock`, then commit.
- Pins GitHub didn't answer for are now retryable errors (exit 1, `"retryable": true`) instead of passing.
- Local `./` actions that call remote actions now block fix and verify runs by default; pass `--migrate-local-actions` (rewrite to `$/`) or `--ignore-local-actions` (warn only).
- New `--json` categories `ref-missing` and `invalid-workflow` (both still exit 1); fix-mode `--json` reports the post-fix state.
- Fix runs never write a lockfile their own verify rejects; moved floating refs stay locked with a non-blocking `ref-moved` warning.
- New: `container-image` warnings for `docker://` steps, job `container:` / `services:` and remote Docker actions (the lockfile can't pin these); a sample CI workflow `.github/workflows/verify-lockfile.yml`; an agent skill via `gh skill install github/gh-actions-lock`; concurrent online pin checks so `--verify` stays about as fast as v0.2.0.

**Revvel action:** if Audrey says yes to adoption, start directly on **v0.3.0** (`gh extension install github/gh-actions-lock --pin v0.3.0`), not v0.2.0, and use the shipped `verify-lockfile.yml` as the shape for a `--verify` step on an existing job. Check the coder/spine workflows for `./` composite actions first, since those now block by default. Still pre-1.0 preview, still needs her OK to touch workflow files, and the look-alike-repo warning above still applies.

**Honesty (2026-10-23):** verified 2026-10-23 (America/Denver) via the GitHub releases API (v0.3.0 body read in full; v0.2.0 still listed as the previous release). Not trialled.

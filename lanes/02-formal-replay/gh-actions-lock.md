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
    "https://github.blog/changelog/2026-10-14-github-actions-workflow-lockfiles-in-public-preview/"
  ],
  "license": "MIT",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "Pin every `uses:` in the existing wr:code / deliver:* workflows (openrouter-coder.yml, revvel-engine-spine.yml, agent-fallback.yml, trusted-bot-auto-approve.yml) to reviewed commits via `.github/workflows/actions.lock`; GitHub then runs the locked commits even if a tag or branch moves. `gh actions-lock --verify` as a step on an existing job fails the run on drift. Same workflows, no second pipeline.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-16"
}
```

**gh-actions-lock** -- GitHub's own `gh` CLI extension for workflow dependency lockfiles, part of its Workflow Dependency Pinning effort. `gh actions-lock` scans `.github/workflows/`, resolves each action (and transitive and reusable-workflow dependencies) to a commit SHA, and writes `.github/workflows/actions.lock`. Once a workflow is onboarded, GitHub Actions requires a lockfile entry for each of its dependencies and runs the recorded commit, even if the tag or branch moves later. Locked pins are sticky and re-checked the way the runner checks them at job start (repo not renamed/transferred, commit still exists, full-version tags still point at it); a failed check blocks the run. Writes are all-or-nothing. `--verify` is the CI check (fails on unused entries and on workflows without entries since v0.2.0); `--verify-local` is offline and never writes; `--relock` re-resolves legitimately moved refs; `--accept-moved` is needed for pins whose commit vanished upstream. Same-repo actions can use `uses: $/…`, which resolves to the running commit and needs no entry (fix runs rewrite `./…` composite refs to `$/…` unless `--no-migrate-local-actions`). A **Require lockfile** policy (public preview) can be set at repo/org/enterprise level, and Dependabot regenerates the lock entry in its own action-update PRs.

v0.2.0 (2026-10-12 13:31 MDT): lockfile schema `v0.0.3`, stricter `--verify`, `--rescan` removed (runs are sticky), rejects expressions in `uses:`, warns on mutable Docker image tags, cooldown honours the Dependabot config. Repo: MIT, created 2026-04-21, last push 2026-10-15 08:42 MDT, ~218 stars.

**Revvel hit:** the deliver:* handoff is only as deterministic as the Actions code it runs. Today a moved `@v4` tag on any action in the coder/spine workflows changes what runs with no diff in revvel-standards. Locking them makes a wr:code run reproducible from the repo SHA alone, and pairs with **agent-approval-check**'s "pin action SHA" note and the replay lane (**chronicle** / **agentape** replay the model; the lockfile pins the runner side). Insertion: commit `actions.lock` + any `$/` rewrites to the existing workflows and add `gh actions-lock --verify` as a step on an existing job (point 5). It touches revvel-standards workflow files, so it needs Audrey's OK before anyone opens that PR.

**Honesty:** CAN-PARTIAL. Verified 2026-10-16 (America/Denver): repo and v0.2.0 release via GitHub API (not a prerelease); README read in full; changelog page 200 and read. The changelog's editor's note (2026-10-14) says the preview covers GitHub Enterprise Cloud, GHE.com data residency, **Team, and Free** plans; GHES is not supported. Pre-1.0 public preview: the README warns the lockfile format, flags, and behaviour may change between releases (schema already moved to v0.0.3). The `$/` syntax is new runner behaviour, so check that every workflow still runs after migration. Locking does not vet the pinned code itself. Not trialled on revvel-standards.

# GitHub Agentic Workflows — Safe Outputs

```json
{
  "id": "gh-aw-safe-outputs",
  "name": "GitHub Agentic Workflows Safe Outputs",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.github.com/gh-aw/reference/safe-outputs/",
    "https://github.github.com/gh-aw/specs/safe-outputs-specification/"
  ],
  "license": "Docs public (GitHub Next / Microsoft Research)",
  "metal": 2,
  "determinism": 4,
  "revvel_hit": "research:complete → wr:code / spec-approved label handoff without agent write tokens (issue #15507 class)",
  "honesty": "CAN",
  "acquired": "2026-08-27"
}
```

Privilege split: agent job is **read-only** and emits structured safe-output requests (add-labels, create-pull-request, …). A separate permissioned job validates and applies them. Built-in `add-labels` / `remove-labels` with allow/block globs, max caps, and required-labels gates.

This is the opposite of “give OpenRouter a PAT and hope.” Structured outputs + least privilege is how you stop prompt-injection from applying `wr:code`.

**Revvel hit:** the stall after `research:complete` is missing a safe label applicator. Map Safe Outputs `add-labels` (allowed: `wr:code`, `spec-approved`, …) onto the existing call chain — do **not** fork `fleet-controller.yml` or invent a second engine. Fits next to `openrouter-coder.yml` which already keys off those labels.

**Honesty:** CAN for the pattern and docs. Adoption into `revvel-standards` still needs a small WR, not a platform rewrite.

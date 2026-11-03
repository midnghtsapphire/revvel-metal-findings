# leanguard

```json
{
  "id": "leanguard",
  "name": "LeanGuard: Lean 4 fail-closed policy gate for agent tool calls",
  "lane": "04-spec-to-code",
  "status": "watching",
  "urls": [
    "https://github.com/DebarghaG/LeanGuard",
    "https://github.com/DebarghaG/LeanGuard/releases/tag/v0.2.0-rc2",
    "https://arxiv.org/abs/2611.02332"
  ],
  "license": "MIT",
  "metal": 3,
  "determinism": 5,
  "revvel_hit": "Pattern (and possible engine) for deliver:* and wr:code tool calls: a deny-unless-permit policy pack in Lean 4 (`permit` / `require` / `forbid`, past-time temporal rules such as read-before-write and quota) is checked by a compiled engine proved equal to a LeanLTL semantics; the host journals the decision to disk before the tool runs, and an approval is bound to the exact arguments plus a backend revision string and can be used once. Fits as one engine behind the existing label gate (insertion point 1), not a new pipeline. Release candidate, Linux + Python 3.12 + Lean toolchain; not on PyPI. Watch, borrow the policy shape and the approval-binding contract.",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-11-03"
}
```

**LeanGuard** (`DebarghaG/LeanGuard`, MIT; repo created 2026-09-07, last push 2026-11-03 08:37 MST, 6 stars). Latest release **v0.2.0-rc2** (pre-release, 2026-09-08 12:50 MDT; tag commit `b5a0e349a8a4e22aaa7c8e1df75f9d3176a6797b`; `pyproject.toml` version `0.2.0rc2`, `license = "MIT"`, Python >= 3.12, Linux only; Lean toolchain `leanprover/lean4:v4.33.1`). **Not on PyPI** (`pypi.org/pypi/leanguard/json` 404); install is `git checkout v0.2.0-rc2 && bash scripts/setup.sh` (pulls elan, LeanLTL, mathlib, builds the native engine). Main moved after the tag (A2A multi-agent merge `79f052f396`, tutorials, 2026-11-02 19:23 MST).

Paper: **LEANGUARD: Lean-Verified Guardrails for Tool-Using Agents**, arXiv **2611.02332** v1 (submitted 2026-11-01 17:26 MST; Sankar, Ganguly, Singh, Hariri, et al.).

What it does (README + abstract): a Python host intercepts each proposed tool call, reads facts from the backend (`snapshot()` returns normalized arguments, units, authoritative state and a **revision string**), and asks the compiled Lean engine for a decision; the decision is written to an on-disk journal **before** the tool runs, and a denied call never reaches the backend. Policies are plain Lean 4 values: everything is denied unless a `permit` matches; every applicable `require` must hold; any `forbid` denies. Rules can use scoped past-time temporal operators over the execution history (e.g. `observed ["read"]` before `write`, `quota`). The decision procedure is **proved equivalent to a LeanLTL semantics**; `serveVerified` serves a pack with a proved safety property. Approvals go through `prepare` → trusted UI → `confirm` → `execute(..., proposal_id=...)`, bound to the exact arguments and the backend revision, single use. Read-only `audit` and `replay` over journals. Core Python has no third-party dependencies; MCP is an optional extra. Denied calls can be returned with the violated rule, or repaired by Lean-side proof search for a nearby admissible call.

Authors' numbers: on Tau-Bench with five Qwen models (0.8B-27B), unguarded agents executed >= 33 policy-forbidden calls, LeanGuard none, with no significant task-success change under feedback; DTap direct prompt-injection success 57.9% -> 5.9%; proof-guided repair found an admissible edit for 88 of 252 argument-value denials, median ~2 ms.

**Revvel hit:** spec-guard / agent-gate / verax already bind approvals to hashes; LeanGuard adds a *checked* policy language with history rules ("tests ran after the last edit", "spec-approved observed before deliver:*", budgets) and the same single-use, argument-and-revision-bound approval contract. Use as a reference shape for the deliver:* rule set and its record (insertion points 1-2); only consider running it once a non-RC release exists. No second pipeline.

**Honesty:** CAN-PARTIAL, watching. Verified 2026-11-03 (America/Denver): repo API (MIT, dates, stars), releases API (v0.2.0-rc2 body), tag commit API, README, `pyproject.toml` and `lean-toolchain` read via API; repo, release and arXiv abs pages 200; PyPI 404. Not built or run (needs the Lean toolchain + mathlib). Benchmark figures are the authors'.

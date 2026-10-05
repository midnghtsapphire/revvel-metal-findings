# linebreak-gate

```json
{
  "id": "linebreak-gate",
  "name": "LineBreak Gate",
  "lane": "04-spec-to-code",
  "status": "active",
  "urls": [
    "https://github.com/Baktun-Studio/linebreak-gate",
    "https://pypi.org/project/linebreak-gate/"
  ],
  "license": "Apache-2.0",
  "metal": 2,
  "determinism": 5,
  "revvel_hit": "spec-approved / wr:code / deliver:* — named-human `spec approve` lands an approved criteria bundle; MCP serves it read-only to the coder; `check` fails closed (exit 0/1/2) until machine criteria pass and manual criteria carry a recorded sign-off",
  "honesty": "CAN-PARTIAL",
  "acquired": "2026-10-05"
}
```

**LineBreak Gate** -- fail-closed CI gate for AI-written code. Two halves: (1) known-CVE dependency blocking with human override recorded in a git-committed audit file; (2) **approved acceptance criteria**. A named human runs `linebreak-gate spec approve <draft> --approver …`, which lands `.linebreak/spec/`; `linebreak-gate mcp` serves that approved bundle over stdio MCP (`list_stories`, `get_story`, `next_story`, `set_story_status`, `check_story`, `spec_status`) and nothing in the bridge can write, edit, or invalidate an approved criterion. `linebreak-gate check` runs `build`/`tests`/`command` criteria for real and blocks `manual` criteria until `linebreak-gate signoff --criterion <id> --approver …`. Exit 0 pass, 1 blocking, 2 config/tool error. Git is the transport: no server, no account. Python; Apache-2.0; PyPI **1.15.0** (uploaded 2026-09-23); repo tip `cb77512eb2fd4f816a2ef53bda0918a1e7df7536` (2026-09-29, synced from upstream v1.15.0); 0★.

**Revvel hit:** this is the closest off-the-shelf shape to the `spec-approved` label: human approval binds criteria, the coder reads them as context before writing code, and the PR check stays red until criteria and sign-offs pass. Wire `check` as the required status check beside existing `deliver:*` CI and map WR acceptance criteria into its draft YAML; do not stand up a second pipeline. Pair with **spec-guard** (hash-bound Approve/Authorize/Complete inside MCP) and **homi-gate** / **aicontracts** (handoff and effects checks).

**Honesty:** CAN-PARTIAL. Verified 2026-10-05 (America/Denver): GitHub live, Apache-2.0 LICENSE, PyPI 1.15.0 live, README documents exit codes and MCP tools. Repo is a publish-bot mirror of a private upstream (Baktun-Studio/linebreak), so issues/PR history are thin; product site linebreakapp.com is commercial-adjacent. Criteria YAML dialect will need mapping to WR fields.

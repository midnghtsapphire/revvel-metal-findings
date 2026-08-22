# revvel-metal-findings

Living scrape of architecture assets closest to the machine, plus deterministic AI, aimed at making [midnghtsapphire/revvel-standards](https://github.com/midnghtsapphire/revvel-standards) ship instead of stall.

This tree **will change**. New scrapes add files. Dead assets get `status: dropped`. Lanes can split.

Maintained by **PedalToTheMetal** for Audrey Evans / MIDNGHTSAPPHIRE.

## Why this repo exists

`revvel-standards` already has the call chain:

`[WR] issue` → research-engine → WR PR → **openrouter-coder (needs `wr:code` / `spec-approved`)** → CI → `ship-to-market` (`deliver:*`)

The stall is the spec-to-code handoff. Findings here are scored on whether they close that gap with **deterministic, near-metal, schema-bound** machinery. Not another essay.

## Layout

```
schema/finding.schema.json   machine record (one shape, every asset)
INDEX.md                     human catalog
MANIFEST.json                machine catalog (regenerated each scrape)
lanes/                       assets grouped by how close they sit to the metal
  00-near-metal/
  01-deterministic-ai/
  02-formal-replay/
  03-agent-runtimes/
  04-spec-to-code/
  05-trials-papers/
hits/revvel-standards.md     insertion points in the SSOT (no second pipeline)
scrapes/YYYY-MM-DD.md        what landed that day
```

## How to use a finding

1. Read the lane file.
2. Check `hits/revvel-standards.md` for the file it should touch (`engines/`, `schemas/`, labels, not a new root process).
3. If it is ready to ship into the SSOT, open a `[WR]` in revvel-standards and apply `wr:code` once the packet exists.

## Honesty

CAN / CAN-PARTIAL / CANNOT / UNKNOWN. Receipt required (URL, commit, test). No vibes.

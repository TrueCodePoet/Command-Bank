---
title: SKILL.md Structure and Authoring Guide
---

# SKILL.md Structure and Authoring Guide

This document focuses exclusively on the `SKILL.md` file format: required frontmatter, recommended body structure, schema expectations, and concise authoring patterns derived from the VS Code Agent Skills reference.

## Required frontmatter

Every skill must start with YAML frontmatter. At minimum include:

- `name` (string): unique, lowercase, hyphen-separated identifier (example: `webapp-testing`). Keep it short (under 64 chars).
- `description` (string): one-line summary of what the skill does and when to use it. Be specific and include trigger phrases if helpful (under 1024 chars).

Example header:

---
name: memory-bank
description: Maintain durable project context in memory-bank/ by consuming and updating core files.
---

Notes:
- The frontmatter is intentionally small — Copilot reads this first for discovery.
- Keep descriptions actionable (include phrases like “run memory bank”, “consume memory bank”, etc.)

## Recommended body sections

Organize the remainder of `SKILL.md` into short, scannable sections. The suggested minimum sections:

- `When to use` — Short trigger phrases and scenarios that should cause the skill to be loaded.
- `Scope and rules` — Explicit read/write boundaries, forbidden edits, and any requirements.
- `Consume (read-only)` — Step-by-step read-only workflow and expected outputs (summary format, headings to include).
- `Update (writes)` — Safe update workflow, minimal-diff rules, `update-log` entry format, and approval requirements.
- `Examples` — Small, runnable examples or sample prompts with expected outputs.
- `Resources` — Relative links to helper scripts, templates, or example files in the skill directory (e.g., `./test-template.js`).

Keep each section concise — prefer numbered steps or short bullets.

## Progressive loading and content organization

Design `SKILL.md` with progressive loading in mind:

1. Frontmatter (name + description) is read first for discovery.
2. Body is loaded only if frontmatter indicates relevance.
3. External resources in the skill directory (scripts, examples) are accessed only when referenced.

Implications:
- Avoid embedding very large examples directly in `SKILL.md`; place them in `examples/` and reference them.
- Put sensitive or large files outside the primary `SKILL.md` body so they aren’t loaded unless explicitly needed.

## Update-log and write rules (if skill writes files)

If the skill performs updates to repository files, define a strict `update-log` format and require explicit user permission for writes. Example `update-log` entry:

```markdown
### 2026-01-12 14:30 UTC
- Updated `activeContext.md` to reflect new sprint goals
- Updated `progress.md` with completed tasks
```

Rules:
- Always append to an `update-log` when changes are made.
- Prefer minimal diffs and avoid wholesale rewrites of existing files.
- Never write outside the skill’s declared scope without explicit user confirmation.

## Examples and minimal templates

Short sample `SKILL.md` skeleton:

---
name: sample-skill
description: Short one-line description and typical trigger phrases.
---

## When to use

- Trigger: "run sample skill" or "help with X"

## Scope and rules

- May read: `project/`, `docs/`
- May write: `project/docs/summary.md` (only with permission)

## Consume (read-only)

1. Read `project/README.md` and `docs/` files
2. Summarize current state in a 5-bullet list

## Update (writes)

1. Create or update `project/docs/summary.md` with a 3-paragraph summary
2. Append an entry to `memory-bank/update-log.md`

## Resources

- `./examples/sample-input.md`
- `./scripts/generate-summary.sh`

## Authoring checklist

- [ ] Frontmatter present and accurate (`name`, `description`)
- [ ] Short `When to use` triggers
- [ ] Explicit `Scope and rules` (read/write boundaries)
- [ ] Minimal examples in `examples/` folder referenced by `SKILL.md`
- [ ] `update-log` format documented if the skill writes files

---

This file is intended to be a compact, reusable authoring reference for contributors writing `SKILL.md` files in this repo.

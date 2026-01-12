---
title: Integrating Agent Skills with the Command Bank Framework
---

# Integrating Agent Skills with the Command Bank Framework

This document explains how Agent Skills fit into the Command Bank repository model and practical integration patterns: where to place skills, how to reference them from agents and commands, testing patterns, and CI/approval guardrails.

## Placement and discovery

- Put project skills in `.github/skills/<skill-name>/SKILL.md` so they are versioned with the repo.
- Keep the Command Bank registry (`.github/available-commands.md`) as the canonical command index — skills complement commands.

Discovery patterns:
- Agents read skill frontmatter (name + description) to decide relevance.
- Use explicit trigger phrases in skill descriptions to improve discovery (e.g., "run memory bank").

## Referencing skills from agents and commands

- VS Code custom agents (`.github/agents/*.agent.md`) can prefer or reference a skill. In agent files include a note or handoff instruction pointing to the skill path: `.github/skills/memory-bank/SKILL.md`.
- Command files in `.github/instructions/` should remain registry-discoverable. If a command benefits from a skill, reference the skill in the command documentation (do not rely on scanning).

Example usages:
- Agent file: prefer skill `.github/skills/memory-bank/SKILL.md` for memory operations.
- Command file: "This command uses Memory Bank skill at `.github/skills/memory-bank/SKILL.md` for context consumption."

## Scope and write safety

- Skills must declare clear scope (which folders/files they may read/write). Document this in `SKILL.md` under `Scope and rules`.
- Skills should avoid touching command-bank framework files (for example `.github/copilot-instructions.md`, `.github/available-commands.md`) unless explicitly allowed.

Write safety recommendations:
- Require explicit user confirmation for writes that will be committed.
- Use feature branches for any automated or agent-driven commits; never auto-commit to `main`.
- Always append to an `update-log` when writing to the `memory-bank/` or other persistent docs.

## Testing and CI

Local validation steps:
1. Dry-run with Planner/Implementer/Reviewer agents in a feature branch.
2. Manually run any helper scripts included with the skill.
3. Verify `update-log` entries are correctly formatted.

CI recommendations (optional, opt-in):
- Add a job that runs generated tests or validates the outputs of skill-driven edits for proposed PRs.
- Keep CI checks scoped and safe (run in sandboxed containers, with no secrets exposed).

## Examples and templates within this repo

- Memory Bank skill: `.github/skills/memory-bank/SKILL.md` (reads/writes `memory-bank/` files)
- Agent example: `.github/agents/memory-bank.agent.md` (prefers the skill and restricts edits to `memory-bank/`)

## Quick integration checklist

- [ ] Place skill under `.github/skills/<skill-name>/`
- [ ] Add frontmatter with `name` and `description` including trigger phrases
- [ ] Document `Scope and rules` and `update-log` format in `SKILL.md`
- [ ] Reference the skill path in any agent (`.agent.md`) that prefers it
- [ ] Use feature branches and explicit confirmation for commits

---

This file is intended to be a pragmatic integration reference so contributors can safely add skills to the Command Bank workflow.

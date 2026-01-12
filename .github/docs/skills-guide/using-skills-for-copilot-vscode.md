---
title: Using Agent Skills with GitHub Copilot in VS Code
---

# Using Agent Skills with GitHub Copilot in VS Code

This document explains how to use and author Agent Skills for GitHub Copilot in VS Code, with practical guidance for the Command Bank project. It assumes the repository follows the Command Bank conventions: a canonical registry, explicit `init command bank` trigger, optional skills under `.github/skills/`, and optional VS Code custom agents under `.github/agents/`.

Contents
- Overview
- Where Skills live in this repo
- Skill file format (frontmatter + content)
- Typical skill lifecycle (consume vs update)
- Example: Memory Bank skill
- Best practices and security
- Testing, validation, and troubleshooting
- Recommended next steps

## Overview

Agent Skills are structured, optional extensions that the Copilot/VS Code agent can load when relevant. They are not a replacement for the canonical command registry (`.github/available-commands.md`) and they do not change the repository’s execution model — scanning is explicit via `init command bank`.

Skills are useful when you have a specialized, stateful workflow (for example, a Memory Bank) or when you want to expose richer behaviour than a single command file provides.

## Where Skills live in this repo

Place skills under `.github/skills/<skill-name>/SKILL.md`. Example: the Memory Bank skill is at `.github/skills/memory-bank/SKILL.md`.

You can link to that file from other docs or agents; the Command Bank repo contains examples in:
- `.github/copilot-instructions.md` — repository routing rules and notes about skills
- `.github/agents/memory-bank.agent.md` — a small agent that prefers the Memory Bank skill

## Skill file format

Skill files are plain Markdown with a small frontmatter header describing the `name` and `description`. The file should clearly document:

- When to use the skill (trigger phrases or situations)
- Scope and rules (what the skill may and may not change)
- Required core files or folders the skill expects to read/write
- Read-only vs write workflows (consume/update)
- Examples and `update-log` entry formats if the skill writes files

Minimal frontmatter example:

---
name: memory-bank
description: Maintain durable project context in memory-bank/ by consuming and updating core files.
---

Then follow with sections for the workflows, file list, and examples.

## Typical skill lifecycle

Consume (read-only):
- Read core files, summarize current state, identify stale or missing pieces, and recommend next steps.

Update (write):
- Read core files, determine minimal changes, write back only affected files, and append a structured `update-log` entry.

Rules:
- Skills must not modify command bank framework files (for example, `.github/copilot-instructions.md`, `.github/available-commands.md`, or files under `.github/instructions/`) unless explicitly allowed.
- Skills should operate on a well-defined folder (for example, `memory-bank/`) and never write outside that scope without explicit user permission.

## Example: Memory Bank skill

See the in-repo example: [.github/skills/memory-bank/SKILL.md](.github/skills/memory-bank/SKILL.md)

Key elements to copy when authoring new skills:

- Clear triggers (e.g., “run memory bank”, “consume memory bank”, “update memory bank”)
- A short mental model or hierarchy diagram showing core file relationships
- A concise `update-log` entry format example
- Explicit scope rules: what folders may be edited

## Best practices

- Keep skills conservative: prefer recommendations over sweeping automated edits.
- Always require human approval for merges to `main` or protected branches.
- Keep frontmatter and first sections concise so an agent can quickly determine if it applies.
- Provide sample prompts and step-by-step workflows inside the skill to guide the agent and human reviewers.
- When in doubt, add a “do not run automatically” warning and require an explicit trigger.

## Security and privacy

- Never include secrets, credentials, or private tokens in skill files or in prompts.
- Do not auto-write or commit files that could leak secrets (for example, CI configs with tokens).
- Limit the agent’s write scope to specific folders and files; prefer append-only logs for change history.

## Testing, validation, and troubleshooting

- Validate skill content by running a dry-run conversation with the Planner/Implementer/Reviewer agents in a feature branch.
- Add small integration checks to CI to ensure skill-driven changes run tests (optional, opt-in).
- If a skill behaved unexpectedly, revert via the version control history and update the skill to add stricter guards.

## Recommended next steps for this repo

1. Add a short README in `.github/skills/` that lists available skills and their purposes.
2. Add a `skills/README.md` entry to link the Memory Bank skill: [.github/skills/memory-bank/SKILL.md](.github/skills/memory-bank/SKILL.md).
3. Consider adding a `work-artifacts/` pattern under `memory-bank/` for safe replay of prompts and outputs.

---

This guide was created from the repository’s current Command Bank conventions (see `.github/copilot-instructions.md` for routing rules) and the `memory-bank` skill example. If you want, I can:

- Create `.github/skills/README.md` and link the Memory Bank skill
- Generate a small template for new skills (frontmatter + sections) at `.github/skills/TEMPLATE_SKILL.md`
- Add a short README snippet showing how to run a skill using the Planner/Implementer/Reviewer agents

Tell me which of the next steps you’d like me to implement now.

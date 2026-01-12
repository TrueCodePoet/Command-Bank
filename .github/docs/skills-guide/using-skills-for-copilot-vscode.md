---
title: Using Agent Skills with GitHub Copilot in VS Code
---

# Agent Skills (detailed)

This document provides an end-to-end, practical guide for authoring, testing, and operating Agent Skills for GitHub Copilot in VS Code. It is tailored for the Command Bank repository conventions (registry-first, explicit `init command bank`, optional `.github/skills/` for project skills) and follows guidance from the official VS Code Agent Skills documentation.

## Quick overview

Agent Skills are a portable, open standard way to bundle instructions, scripts, examples, and resources so skills-capable agents (like GitHub Copilot in VS Code, the Copilot CLI, and the Copilot coding agent) can load specialized behavior on demand.

Use skills when you want:
- Reusable, task-focused capabilities that include code examples or helper scripts
- Workflows that are richer than a single prompt (testing, debugging, memory management)
- Portability across skills-aware agents and environments

Skills complement the Command Bank registry (`.github/available-commands.md`). Keep the registry for command discovery and use skills for richer, self-contained capabilities.

## Skill types and recommended placement

- Project skills: store under `.github/skills/<skill-name>/SKILL.md` (recommended for team use, versioned with the repo).
- Personal skills: store under `~/.copilot/skills/` (for user-specific shortcuts).

Each skill should be a directory containing a `SKILL.md` file and optional resources (scripts, templates, examples). Keep each skill focused and scoped.

## `SKILL.md` required structure

1. YAML frontmatter header (required)
   - `name`: unique, lowercase, hyphen-separated identifier (e.g., `webapp-testing`).
   - `description`: short, specific description of capability and when to use it.

Example:

---
name: memory-bank
description: Maintain durable project context in memory-bank/ by consuming and updating core files.
---

2. Body: clear sections that explain usage and constraints. Recommended headers:
- `When to use` — trigger phrases and scenarios
- `Scope and rules` — read/write boundaries and forbidden edits
- `Consume (read-only)` — step-by-step read-only workflow and outputs
- `Update (writes)` — safe update steps and `update-log` format
- `Examples` — sample prompts, inputs, and outputs
- `Resources` — links to scripts or templates in the skill folder

## How Copilot loads skills (progressive disclosure)

Copilot uses a three-level loading model to keep context efficient:

1. Discovery: Copilot reads the frontmatter (only `name` and `description`) across skills to decide relevance.
2. Instruction load: If a skill looks relevant, Copilot loads the `SKILL.md` body into the model context.
3. Resource access: Additional files (scripts, examples) are accessed only when explicitly referenced.

Implications:
- Keep frontmatter concise and specific to improve signal for discovery.
- Put larger examples or helpers as separate files in the skill directory (they are only pulled when needed).

## Authoring best practices

- Make `description` actionable: include common trigger phrases and short examples.
- Be explicit about scope: list exactly which folders/files the skill may read or write.
- Prefer step-by-step procedures over long essays. Agents favor short actionable instructions.
- Provide minimal, runnable examples and templates for common tasks.
- If the skill writes files, require explicit user intent before writing and define a clear `update-log` format to track changes.

## Security and approvals

- Treat scripts as sensitive: require the user to confirm any script execution.
- Use VS Code's auto-approve allow-lists carefully; prefer manual approval for anything that can change the repo or environment.
- Never include secrets, credentials, or tokens in skill files or helper scripts.
- Enforce human approval for merges to protected branches; do not auto-commit to `main`.

## Packaging and sharing

- To reuse a skill, copy its directory into another repo's `.github/skills/` and review scripts and instructions before use.
- Consider publishing stable, general-purpose skills in a shared org repository for discovery.

## Testing and validation

1. Dry-run conversations: use your Planner/Implementer/Reviewer agents to exercise the skill in a feature branch.
2. Manual script validation: run helper scripts locally in an isolated environment before allowing agent-driven execution.
3. Optional CI: add opt-in CI jobs that run generated tests or validate the outputs of skill-driven edits.

## Example templates (suggested files)

- `.github/skills/README.md` — list and short descriptions of skills in the repo.
- `.github/skills/TEMPLATE_SKILL.md` — starter template for new skills.

Minimal `TEMPLATE_SKILL.md` starter:

---
name: skill-name
description: One-line description of what this skill does and when to use it.
---

## When to use

Short trigger phrases and situations.

## Scope and rules

What this skill may and may not change.

## Consume (read-only)

Steps for reading and summarizing context.

## Update (writes)

Steps for safe updates and an `update-log` example.

## Examples

Sample prompts and expected outputs.

## Resources

List helper scripts or templates (relative paths).

---

## Recommended next steps (I can implement these)

1. Add `.github/skills/README.md` to index skills in-repo.
2. Add `.github/skills/TEMPLATE_SKILL.md` as the authoring template.
3. Add a short snippet in the main `README.md` showing how to enable `chat.useAgentSkills` and where skills live.

If you want, I can create the template and skills README and commit them now.
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

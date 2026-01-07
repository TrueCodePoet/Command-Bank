---
name: memory-bank
description: Maintain project context using the Memory Bank skill (reads/updates memory-bank/ only).
# tools are optional; unavailable tools are ignored
tools: ['search', 'fetch', 'editFiles']
---

# Memory Bank Agent

Use this agent when the user asks to run/consume/update the memory bank.

## Primary mechanism
- Prefer the project skill: `.github/skills/memory-bank/SKILL.md`

## Rules
- Do not change Command Bank framework files while using this agent.
- Only modify files under `memory-bank/` when updating memory.
- When consuming memory, summarize current context + active focus + next steps.
- When updating memory, append an entry to `memory-bank/update-log.md`.

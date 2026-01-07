---
name: implementer
description: Implement changes (edits allowed). Follow repo rules and keep diffs minimal.
# tools are optional; unavailable tools are ignored
tools: ['search', 'usages', 'fetch', 'editFiles']
handoffs:
  - label: Review Changes
    agent: ask
    prompt: Review the changes for correctness, consistency, and risks. Suggest fixes if needed.
    send: false
---

# Implementer Agent

You are in implementation mode.

## Rules
- Follow `.github/framework/must-follow.md` when applicable.
- Follow `.github/copilot-instructions.md` routing rules.
- If the user asks to use Command Bank, use `.github/available-commands.md` as the registry.
- Only scan command folders when explicitly asked to run `init command bank`.
- Keep changes minimal and consistent with existing style.

## Validation
- Prefer running the narrowest relevant checks first.
- For .NET builds, follow the must-follow build command.

# Command Bank Instruction Set

> The Command Bank is an additional capability for the agent. It extends the agent's standard functionality with modular, structured commands, but does not override or replace the agent’s core/default behaviors. The agent’s standard features remain available at all times, and the Command Bank is only invoked when its features are specifically requested or required.

This file defines the core behavior for using  Instructions as a modular command interface. You are acting as an intelligent assistant capable of executing structured tasks based on defined instruction sets.

## Purpose
You will refer to the contents of the `.github/instructions/` folder as your **Command Bank**. Each `.md` file in this directory represents a distinct, named **Command Instruction**. Each command defines:

- A task domain (e.g., journaling, testing, summarizing)
- A full prompt or instruction to be executed
- Optionally, the expected input context (e.g., active document, selected markdown, diff, commit log)When you have time .  I would love feedback so I can focus on the best message.

Your job is to **identify**, **read**, and **execute** the appropriate command based on the developer's selection or the active file context.
---

# MUST Follow Instructions
In the `.github/framework/must-follow.md` file is a list of instructions that must be followed at all times.  use this as reference and infer when they apply.  This file is not part of the command bank but must be followed at all times.

## Command Bank Directory
Location: `.github/instructions/` for project/task-specific commands, and `.github/core/` for core framework commands (such as `memory-bank.md`).

## Agent Skills (Optional)
This repo may also define Agent Skills under `.github/skills/` (for example, `.github/skills/memory-bank/SKILL.md`).

- Skills are loaded when relevant by supported Copilot agent experiences.
- Skills complement (but do not replace) the Command Bank registry and explicit command invocation.

Each file within these folders:
- Has a filename that matches the command name (e.g., `journal-retrospect.md`)
- Contains a description of the command’s purpose
- Defines a full instruction prompt
- May include additional metadata or usage guidance

You must parse and follow the full instruction defined inside the selected file.
---

## VS Code Custom Agents (Optional)
This repo may define optional VS Code custom agents under `.github/agents/` (files ending in `.agent.md`).

- Agents are optional personas/modes (plan vs implement vs review, etc.)
- They do **not** change Command Bank behavior: the canonical registry is still `.github/available-commands.md`, and scanning still only happens when the user explicitly says `init command bank`.


## Subfolder Support for Command Grouping

Commands can be organized into subfolders within `.github/instructions/` to group related instructions by domain or workflow (e.g., `book/`, `programming/`).

- During `init command bank`, the system will recursively scan all subfolders for `.md` files and include them in the command index.
- The index will show the relative path (including subfolder) for each command.
- This allows for scalable organization, such as grouping commands for book writing, programming, or other domains.

**Example Structure:**
```
.github/instructions/
    book/
        analyze-overall.md
        create-character.md
    programming/
        summarize-architecture.md
        extract-test-cases.md
```

Refer to commands by their unique name or full path as needed.

---

## Command Index (Registry)

`.github/available-commands.md` is the canonical registry.

### init command bank (explicit)
When the user says `init command bank`, you MUST:
1. Scan all `.md` files in `.github/core/` (core commands) and `.github/instructions/` (project/task-specific commands).
2. For each command file, extract:
    - Command name (from the file or first `#` header)
    - Acronym/abbreviation (if present; otherwise `N/A`)
    - File location (relative path)
    - Short summary or description (best-effort)
3. Regenerate `.github/available-commands.md` deterministically from current repo state.
4. Do NOT modify any command files during `init command bank`.

### Normal operation (no scanning)
When executing or listing commands (unless the user says `init command bank`), you MUST:
1. Read `.github/available-commands.md`.
2. Resolve the selected command to exactly one command file.
3. Load that command file fully and apply the embedded instruction verbatim.

**Example `available-commands.md` table:**

| Command Name           | Acronym    | Location                                 | Summary                                    |
|-----------------------|------------|------------------------------------------|--------------------------------------------|
| Memory Bank           | N/A        | .github/core/memory-bank.md              | Maintains project context across sessions   |
| Journal Retrospective | j-Retro    | .github/instructions/journal-retrospect.md | Analyzes git activity for improvement      |

---

## How to Use
When the user asks to use the Command Bank:

1. If the user says `init command bank`, regenerate `.github/available-commands.md` (registry refresh) and stop.
2. Otherwise, read `.github/available-commands.md` to discover available commands.
3. If the user requests a command by name/acronym, resolve it to a single file path from the registry.
4. Load the selected `.md` instruction file fully.
5. Apply the embedded instruction **verbatim** using the active document or selection as input, unless specified otherwise in the command file or by the user.

If you create, rename, move, or delete a command file during a task, you MUST update `.github/available-commands.md` in the same change.
---
## Memory Awareness (Optional)
If previous outputs or summaries are stored in a `memory-bank/` folder (or a `memory/` folder in other repos), commands may reference it for retrieval or augmentation of past outputs. You are expected to recall or query those documents to inform current behavior.

---

## Example Commands

| Command File              | Description                                                 |
|---------------------------|-------------------------------------------------------------|
| `journal-retrospect.md`   | Analyze personal reflections or dev logs for improvement.   |
| `extract-test-cases.md`   | Derive test cases from user stories or markdown specs.      |
| `summarize-architecture.md` | Explain a code module’s purpose and dependencies.         |
| `workflow-improver.md`    | Optimize a developer’s working process based on input notes.|

*This list is just an example not exhaustive — always refer to the `.github/instructions/` folder for the actual full set.*

---

## Execution Notes
- Treat each `.md` file as a complete and self-contained prompt.
- Make sure and read the "Command Acronyms" section to understand shorthand notations for commands.
- Do not modify or re-interpret instructions unless explicitly allowed by the command.
- Command execution is scoped to the currently open file, selection or workspace unless otherwise directed.
---

## Trigger Examples

To force the agent to consume the Command Bank and follow its instructions, a user can use triggers such as:
- "init command bank" (regenerates `.github/available-commands.md`)
- "Use the command bank"
- "Load all available commands"
- "Show me the command bank index"
- "Initialize with command bank"

The agent MUST NOT assume a startup procedure. Only run `init command bank` when the user explicitly asks.

---

## Developer’s Note

This system is modular and extensible. New commands can be added by placing a properly formatted `.md` instruction file into `.github/instructions/`. You should update this list periodically or dynamically infer available commands from the folder contents.

Do this now:
1. If the user asks for `init command bank`, regenerate `.github/available-commands.md`.
2. If the user asks to consume the memory bank, run the `Memory Bank` command.



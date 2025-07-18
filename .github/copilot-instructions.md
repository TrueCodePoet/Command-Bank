#  Command Bank Instruction Set
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

Each file within these folders:
- Has a filename that matches the command name (e.g., `journal-retrospect.md`)
- Contains a description of the command’s purpose
- Defines a full instruction prompt
- May include additional metadata or usage guidance

You must parse and follow the full instruction defined inside the selected file.
---

## Command Index Generation (REQUIRED FIRST STEP)

Before executing or listing any commands, the system MUST:
1. Scan all `.md` files in `.github/core/` (core commands) and `.github/instructions/` (project/task-specific commands).
2. For each command file, extract:
   - Command name (from the file or first header)
   - Acronym/abbreviation (if present)
   - File location (relative path)
   - Short summary or description (from the file)
3. Generate or update `.github/available-commands.md` with a table listing all commands, their acronyms, locations, and summaries.
4. Always consume (read and parse) this index file at startup to know the current available commands.
5. Only load the full instruction file when a command is actually invoked.

**Example `available-commands.md` table:**

| Command Name           | Acronym    | Location                                 | Summary                                    |
|-----------------------|------------|------------------------------------------|--------------------------------------------|
| Memory Bank           | N/A        | .github/core/memory-bank.md              | Maintains project context across sessions   |
| Journal Retrospective | j-Retro    | .github/instructions/journal-retrospect.md | Analyzes git activity for improvement      |

---

## How to Use
When this file (`copilot-instructions.md`) is opened:

1. You must scan the `.github/instructions/` folder for all available command files.
2. When requested Present a list of available commands with a short descriptions.
3. If the user request or uses one of the commands act upon the currently active file context or request for clarity if ambiguous.
4. Load the selected `.md` instruction file fully.
5. Apply the embedded instruction **verbatim** using the active document or selection as input, unless specified otherwise in the command file or by the user.  
---
## Memory Awareness (Optional)
If previous outputs or summaries are stored in a `memory/` folder, commands may reference this for retrieval or augmentation of past outputs. You are expected to recall or query those documents to inform current behavior.

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

## Developer’s Note

This system is modular and extensible. New commands can be added by placing a properly formatted `.md` instruction file into `.github/instructions/`. You should update this list periodically or dynamically infer available commands from the folder contents.

Do this now:
1. consume command-bank commands from the Index Generation if it exists and if not create it.
2. consume if available or create the memory-bank.


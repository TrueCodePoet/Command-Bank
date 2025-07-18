# Command Bank

> A modular framework for managing reusable AI
 
## Available Commands
| Command File              | Acronym  | Description                                                  |
|## Learn More

### Related Resources
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)

### Key Concepts
- **Command Bank**: Structured AI instruction system
- **Memory Bank**: Project context persistence for AI agents
- **Framework Rules**: Global constraints and standards
- **Command Acronyms**: Quick reference shortcuts for commands

---

> *Use markdown. Program AI. Share intelligence.*  
> This is the future of prompt engineering and AI-assisted development workflows.-----------------|----------|--------------------------------------------------------------|
| `journal-retrospect.md`   | `j-Retro` | Analyzes dev reflections, git logs, and commit activity for behavioral insights and improvement suggestions |
| `memory-bank.md`          | N/A      | Comprehensive project context management system that maintains documentation across AI sessions |

### Command Features

- **Journal Retrospective**: Uses git commands (read-only) to analyze commit history, emotional patterns in development, and suggests process improvements
- **Memory Bank**: Structured documentation system with core files (projectbrief.md, productContext.md, etc.) that helps AI maintain project understanding across sessionsions that turn GitHub Copilot (or any AI agent) into a programmable assistant inside your editor.

Command Bank lets you define a structured set of **declarative commands** as markdown-based instruction files. These commands can be version-controlled, shared, and executed directly within VS Code to enhance development workflows using AI.

The system provides both **Commands** (for specific AI tasks) and **Memory Bank** (for project context persistence across AI sessions).

---

## Why Command Bank?

Traditional Copilot usage relies on inline code completions or manually crafted prompts. The Command Bank elevates this by:

- Modularizing AI instructions into discrete command files
- Allowing **task-oriented execution** across dev, docs, infra, and process work
- Making AI behavior predictable, reusable, and auditable
- Enabling **team-wide prompt engineering** with collaboration and versioning

---

##  Project Structure

```
.github/
├── copilot-instructions.md     # Entry point: explains how the command system works
├── framework/
│   └── must-follow.md         # Core instructions that must always be followed
└── instructions/              # Command Bank - individual AI command files
    ├── journal-retrospect.md  # Analyzes dev reflections and git activity
    └── memory-bank.md         # Manages project context across AI sessions
```

### Key Components

- **`copilot-instructions.md`** - The main controller that defines how AI agents consume and execute commands
- **`framework/must-follow.md`** - Global rules and constraints applied to all AI operations
- **`instructions/`** - The Command Bank containing individual command files
- **Memory Bank** - Optional project memory system for maintaining context across AI sessions



---

## 📘 How It Works

1. **`copilot-instructions.md`** defines the behavior of the command bank and how to execute commands.
2. Each `.md` file in `.github/instructions/` is a **self-contained AI instruction** for a specific task.
3. The **framework** folder contains global rules that apply to all AI operations.
4. You open a source file in VS Code (or select code), then reference one of these command files.
5. Trigger your AI agent (GitHub Copilot, etc.) and it will read the instruction and use your current file/selection as the execution context.
6. Commands can include acronyms for quick reference (e.g., `j-Retro` for journal retrospective).

### Command Execution Flow
1. AI agent reads `copilot-instructions.md` to understand the system
2. AI scans `.github/instructions/` for available commands
3. AI loads the requested command file and follows its instructions
4. AI applies the command to the current context (active file, selection, etc.)
5. AI follows any applicable rules from `framework/must-follow.md`

---

## Example Commands

| Command File              | Description                                                  |
|---------------------------|--------------------------------------------------------------|
| `journal-retrospect.md`   | Analyzes dev reflections for behavior patterns and suggestions |
| `summarize-architecture.md` | Describes a file/module’s purpose and dependencies        |
| `convert-java-to-csharp.md` | Translates Java source into idiomatic C# code             |
| `generate-readme.md`      | Builds a complete README from a source file or component     |
| `extract-test-cases.md`   | Creates test scenarios from feature specs or markdown        |

> View the full list in [`copilot-instructions.md`](./instructions/copilot-instructions.md)

---

## Memory Bank System

The Memory Bank is a sophisticated project context management system designed for AI agents that reset between sessions. It maintains structured documentation to ensure continuity and effectiveness.

> **Note**: The Memory Bank concept is inspired by the excellent work detailed in ["Efficient AI Collaboration with Memory Bank"](https://blog.wadan.co.jp/en/tech/efficient-ai-collaboration-with-memory-bank) by Wadan's engineering team.

### Core Memory Files
- **`projectbrief.md`** - Foundation document defining core requirements and goals
- **`productContext.md`** - Why the project exists and how it should work
- **`activeContext.md`** - Current work focus and recent changes
- **`systemPatterns.md`** - Architecture and technical decisions
- **`techContext.md`** - Technologies, setup, and constraints
- **`progress.md`** - Current status and what's left to build

### Memory Workflows
- **Plan Mode**: Read memory bank → verify context → develop strategy
- **Act Mode**: Check context → update documentation → execute task
- **Update Triggers**: New patterns, significant changes, or explicit requests

---

## Usage Tips

### Getting Started
1. Copy the `.github` folder structure into your project
2. Reference `copilot-instructions.md` when working with AI agents
3. Use command acronyms for quick access (e.g., `j-Retro` for journal retrospective)
4. Set up Memory Bank files if you want persistent project context

### Best Practices
- Use `Ctrl+P` in VS Code to quickly navigate to command files
- Pin commonly used commands in your workspace
- Use rich markdown formatting in instruction files to guide AI output structure
- Customize the `framework/must-follow.md` file for your project's specific requirements
- Regularly update Memory Bank files when significant changes occur

### Working with Commands
- Commands use the current active file or selection as context
- Some commands (like journal-retrospect) interact with git history
- Memory Bank commands help maintain project context across AI sessions
- Follow command-specific instructions for best results

---

## Example Workflow
### Starting command-bank
1. Open your project in VS Code
2. Enter: "Enable the command-bank" into your agent command window and hit enter.
3. you should see the agent consuiming avaiable commands.

### Once the command-bank is enabled you can create the memory-bank
1. Enter: "Implement the memory bank" into your agent command window and hit enter.
2. you should see the agent consuiming or creating the memory-bank.
> if you have multiple folders or projects in the workspace just tell the agent which one.
> Enter: for the XYZ project Implement the memory bank

### Using Journal Retrospective
1. Open your project in VS Code
2. Reference `journal-retrospect.md` command in your AI agent
3. The AI will analyze git history, commit patterns, and development activity
4. Receive insights on emotional patterns, technical decisions, and improvement suggestions

### Setting Up Memory Bank
1. Create a `memory-bank/` folder in your project root
2. Use the `memory-bank.md` command to initialize core documentation files
3. AI agents will maintain and update these files across sessions
4. Enjoy consistent project context and improved AI assistance

---

## Customizing the Command Bank

### Adding New Commands
- Add new `.md` instruction files to `.github/instructions/`
- Include command acronyms for quick reference
- Each command should include:
  - A clear title and description
  - Expected input context
  - Structured instruction prompt
  - Formatting rules or output expectations

### Framework Configuration
- Modify `.github/framework/must-follow.md` for project-specific global rules
- Examples: coding standards, build commands, deployment procedures
- These rules apply to all AI operations regardless of the specific command

### Memory Bank Customization
- Adapt core memory files to your project type
- Add additional context files for complex features
- Create project-specific documentation patterns
- Integrate with your existing development workflow

---

## Contributing

1. Fork this repository
2. Add new `.md` instruction files to `.github/instructions/`
3. Follow existing formatting conventions:
   - Include command acronyms where appropriate
   - Provide clear descriptions and expected contexts
   - Use structured markdown formatting
4. Test your commands with AI agents
5. Submit a PR with a description of your command and use case

### Command Development Guidelines
- Focus on reusable, task-oriented instructions
- Make commands self-contained and well-documented
- Consider both individual developer and team use cases
- Provide examples where helpful

---

## License

MIT License — see [`LICENSE`](./LICENSE)

---

## Learn More

- GitHub Copilot → [docs](https://docs.github.com/en/copilot)
- Prompt Engineering Best Practices → [OpenAI Cookbook](https://github.com/openai/openai-cookbook)
- Prompt Engineering with AI Agents → [awesome-prompt-engineering](https://github.com/dair-ai/Prompt-Engineering-Guide)

---

> *Use markdown. Program Copilot. Share intelligence.*  
> This is the future of prompt engineering in your team’s editor.

## Command Usage Examples

### 1. Journal Retrospective (`journal-retrospect.md` / `j-Retro`)
**Purpose:** Analyze your recent development activity for emotional tone, workflow patterns, and improvement areas.

**How to use:**
**Example prompt:**
> "j-Retro my last week of commits."

---

### 2. Memory Bank (`memory-bank.md`)
**Purpose:** Maintain and update structured project documentation so the AI can retain context across sessions.

**How to use:**
**Example prompt:**
> "Update the memory bank to reflect the latest architecture changes and current work focus."

---

For more details, see the full instructions in each command file under `.github/instructions/`.

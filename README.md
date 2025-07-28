# Command Bank

> **Command Bank is a next-generation system for managing, sharing, and executing structured AI instructions in your development workflow.**
>
> While this implementation targets GitHub Copilot, the concept is platform-agnostic and works with most markdown-capable AI agents or editor extensions (such as Cline, Cusor, or other custom LLM integrations).
>
> Instead of relying on ad-hoc prompts or scattered documentation, Command Bank lets you define, organize, and version-control reusable AI commands as markdown files. These commands can automate code reviews, generate documentation, analyze git history, enforce standards, and much more—directly from your editor.
>
> **Why do you need it?**
> - Modern AI agents (like Copilot) are powerful, but their value is limited by the quality and consistency of their instructions. Command Bank brings order, auditability, and collaboration to prompt engineering.
> - It enables teams to build a shared library of best-practice AI workflows, making AI assistance predictable, repeatable, and tailored to your project or organization.
>
> **Why use Command Bank?**
> - **Modular & Scalable:** Organize commands by domain, project, or workflow using subfolders and dynamic indexing.
> - **Team Collaboration:** Share, review, and improve AI instructions as code—just like any other part of your project.
> - **Persistent Context:** Integrate with a Memory Bank to maintain project knowledge across sessions and contributors.
> - **Plug-and-Play:** Works with any markdown-capable AI agent or editor extension.
> - **Transparency & Auditability:** Every command is versioned, documented, and reviewable.
>
> *Command Bank transforms AI from a black box into a programmable, collaborative teammate—empowering you to build smarter, faster, and with greater confidence.*

## Available Commands

| Command File             | Acronym   | Description                                                                                       |
|-------------------------|-----------|---------------------------------------------------------------------------------------------------|
| `journal-retrospect.md` | j-Retro   | Analyzes dev reflections, git logs, and commit activity for behavioral insights and improvement    |
| `memory-bank.md`        | N/A       | Comprehensive project context management system that maintains documentation across AI sessions    |

## Available Commands (Example)

| Command File                                 | Acronym | Description                                                        |
|----------------------------------------------|---------|--------------------------------------------------------------------|
| `analysis/find-logical-fallacies.md`         | FLF     | Detects and explains logical fallacies in arguments or text        |
| `analysis/compare-and-contrast.md`           | CNC     | Compares and contrasts items in a Markdown table                   |
| `learning/create-quiz.md`                    | CQZ     | Generates review questions from subject and learning objectives     |
| `analysis/extract-questions.md`              | EXQ     | Extracts questions and analyzes their effectiveness                |
| `programming/improve-prompt.md`              | IMP     | Refines and enhances LLM/AI prompts for clarity and effectiveness  |
| `content/summarize-content.md`               | SUM     | Summarizes content with key points and takeaways                   |
| `content/extract-insights.md`                | EXINS   | Extracts powerful insights from text                               |
| `security/report-finding-create.md`          | CRF     | Creates a professional security finding for assessment reports     |
| `journal-retrospect.md`                      | j-Retro | Analyzes git activity for workflow and emotional insights          |
| `core/memory-bank.md`                        | N/A     | Maintains project context across sessions                          |

---

## New Features & Concepts

### 🗂️ Subfolder Support & Command Grouping
- Commands can be organized into subfolders within `.github/instructions/` (e.g., `book/`, `programming/`)
- The system recursively scans all subfolders for `.md` files and includes them in the command index
- Subfolders allow scalable organization by domain, workflow, or project area
- The command index lists the relative path (including subfolder) for each command

### 🔄 Dynamic Command Indexing
- On startup, the system generates or updates `.github/available-commands.md` with a table of all commands, acronyms, locations, and summaries
- The index is always consumed to know the current available commands
- Only the selected command file is loaded fully when invoked

### 🧠 Memory Awareness
- If a `memory/` folder exists, commands may reference it for context or to augment outputs
- The memory bank is always read at the start of a session or when context is needed

---

## Learn More

### Related Resources
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)

### Key Concepts
- **Command Bank**: Structured AI instruction system
- **Memory Bank**: Project context persistence for AI agents
- **Framework Rules**: Global constraints and standards
- **Command Acronyms**: Quick reference shortcuts for commands
- **Subfolder Grouping**: Organize commands by domain or workflow
- **Dynamic Indexing**: Always up-to-date command list

---

> *Use markdown. Program AI. Share intelligence.*
> This is the future of prompt engineering and AI-assisted development workflows.

### Command Features

- **Journal Retrospective**: Uses git commands (read-only) to analyze commit history, emotional patterns in development, and suggests process improvements
- **Memory Bank**: Structured documentation system with core files (projectbrief.md, productContext.md, etc.) that helps AI maintain project understanding across sessions

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
└── instructions/              # Command Bank - individual AI command files and subfolders
    ├── journal-retrospect.md  # Analyzes dev reflections and git activity
    ├── memory-bank.md         # Manages project context across AI sessions
    ├── book/                  # Book writing commands (grouped)
    │   ├── create-character.md
    │   └── analyze-overall.md
    └── programming/           # Programming-related commands (grouped)
        ├── summarize-architecture.md
        └── extract-test-cases.md
```

### Key Components

- **`copilot-instructions.md`** — The main controller that defines how AI agents consume and execute commands
- **`framework/must-follow.md`** — Global rules and constraints applied to all AI operations
- **`instructions/`** — The Command Bank containing individual command files and subfolders for grouping
- **Memory Bank** — Optional project memory system for maintaining context across AI sessions



---

## 📘 How It Works

1. **`copilot-instructions.md`** defines the behavior of the command bank and how to execute commands.
2. Each `.md` file in `.github/instructions/` or any subfolder is a **self-contained AI instruction** for a specific task.
3. The system recursively scans all subfolders for available commands and generates an up-to-date index.
4. The **framework** folder contains global rules that apply to all AI operations.
5. You open a source file in VS Code (or select code), then reference one of these command files.
6. Trigger your AI agent (GitHub Copilot, etc.) and it will read the instruction and use your current file/selection as the execution context.
7. Commands can include acronyms for quick reference (e.g., `j-Retro` for journal retrospective).

### Command Execution Flow
1. AI agent reads `copilot-instructions.md` to understand the system
2. AI scans `.github/instructions/` and all subfolders for available commands
3. AI generates or updates `.github/available-commands.md` as the command index
4. AI loads the requested command file and follows its instructions
5. AI applies the command to the current context (active file, selection, etc.)
6. AI follows any applicable rules from `framework/must-follow.md`

---

## Example Commands

| Command File                | Description                                                    |
|----------------------------|----------------------------------------------------------------|
| `journal-retrospect.md`    | Analyzes dev reflections for behavior patterns and suggestions  |
| `summarize-architecture.md`| Describes a file/module’s purpose and dependencies             |
| `convert-java-to-csharp.md`| Translates Java source into idiomatic C# code                  |
| `generate-readme.md`       | Builds a complete README from a source file or component        |
| `extract-test-cases.md`    | Creates test scenarios from feature specs or markdown           |

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

## Usage Examples

### Example 1: Summarize Content (SUM)
**Command:** `content/summarize-content.md`
**Input:** select or Paste a technical article or documentation.  Then type : Summarize Content.
**Output:**
```
ONE SENTENCE SUMMARY:
A concise summary of the article in 20 words.

MAIN POINTS:
1. Key point one
2. Key point two
...

TAKEAWAYS:
1. Major takeaway one
2. Major takeaway two
...
```

---

### Example 2: Find Logical Fallacies (FLF)
**Command:** `analysis/find-logical-fallacies.md`
**Input:** select or Paste an argumentative essay or debate transcript. then type FLF
**Output:**
```
- Fallacy: Appeal to Probability
  Explanation: Assumes something is true because it is likely.
  Example: "It will probably rain, so we should cancel."
- Fallacy: Non Sequitur
  Explanation: Conclusion does not logically follow premise.
  Example: "She drives a BMW, so she must be rich."
```

---

### Example 3: Create Quiz (CQZ)
**Command:** `learning/create-quiz.md`
**Input:** Select or Provide subject and learning objectives.  Then type CQZ
**Output:**
```
Subject: Machine Learning
Learning Objective: Understand supervised vs. unsupervised learning
  - What is the main difference between supervised and unsupervised learning?
  - Give an example of a supervised learning algorithm.
  - Why might you choose unsupervised learning?
```

---

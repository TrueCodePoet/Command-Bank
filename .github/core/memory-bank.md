# Memory Bank

## Agent Skill (preferred)

If Agent Skills are supported in your environment, prefer the project skill at:

- `.github/skills/memory-bank/SKILL.md`

Use this command as the explicit entry point when a user asks to "run/consume/update memory bank".

## AI Role and Expected Output

When running this command, the AI should:
- Read and understand the core memory bank files in the `memory-bank/` folder.
- Summarize the current project context, recent changes, and active work focus.
- Identify missing or outdated documentation and suggest updates.
- Clarify any ambiguous or incomplete information.
- Output results in clear markdown format, such as:
  - A summary section
  - A checklist of missing or outdated files
  - Next steps for documentation or project focus

---

## When to Update the Memory Bank

**Update the memory bank whenever any of the following occur:**
- After implementing significant changes or refactors
- When new project patterns or technical decisions are discovered
- At the end of a sprint, milestone, or major feature
- When context or requirements need clarification
- When the user requests with **update memory bank** or **consume memory bank**

> **Tip:** Regular updates ensure the memory bank remains a reliable source of project truth and context for all contributors and AI agents.

---

This command is only run when explicitly requested. Do NOT assume a startup procedure.

When triggered to **consume** or **update** the memory bank, review all core files (listed below) to understand and maintain project context.

## Memory Bank Structure
The Memory Bank consists of required core files and optional context files, all in Markdown format. Files build upon each other in a clear hierarchy:
```mermaid
flowchart TD
    PB[projectbrief.md] --> PC[productContext.md]
    PB --> SP[systemPatterns.md]
    PB --> TC[techContext.md]
    PC --> AC[activeContext.md]
    SP --> AC
    TC --> AC
    AC --> P[progress.md]
```

### Core Files (Required)
1. `projectbrief.md`
   - Foundation document that shapes all other files
   - Created at project start if it doesn't exist
   - Defines core requirements and goals
   - Source of truth for project scope
2. `productContext.md`
   - Why this project exists
   - Problems it solves
   - How it should work
   - User experience goals
3. `activeContext.md`
   - Current work focus
   - Recent changes
   - Next steps
   - Active decisions and considerations
4. `systemPatterns.md`
   - System architecture
   - Key technical decisions
   - Design patterns in use
   - Component relationships
5. `techContext.md`
   - Technologies used
   - Development setup
   - Technical constraints
   - Dependencies
6. `progress.md`
   - What works
   - What's left to build
   - Current status
   - Known issues
7. `update-log.md`
   - Chronological log of all memory bank updates
   - Each entry should include:
     - Date and time of update
     - Summary of recent changes or additions
     - Who made the update (if applicable)
   - Helps track the evolution of project context and documentation

### Additional Context
Create additional files/folders within memory-bank/ when they help organize:
- Complex feature documentation
- Integration specifications
- API documentation
- Testing strategies
- Deployment procedures
- ToDo lists

---

## How to Use `update-log.md`

- Every time you update any memory bank file, add a new entry to `update-log.md`.
- Each entry should include:
  - The current date and time (e.g., 2025-07-18 14:30 UTC)
  - A brief summary of what was changed or added
  - (Optional) Your name or initials for team tracking
- Example entry:

  ```markdown
  ### 2025-07-18 14:30 UTC
  - Updated `activeContext.md` to reflect new sprint goals
  - Added new API documentation to `techContext.md`
  - (JDS)
  ```

- This log helps maintain a transparent history of project context evolution and supports onboarding and audits.

---

## Core Workflows

### Plan Mode
```mermaid
flowchart TD
    Start[Start] --> ReadFiles[Read Memory Bank]
    ReadFiles --> CheckFiles{Files Complete?}
    CheckFiles -->|No| Plan[Create Plan]
    Plan --> Document[Document in Chat]
    CheckFiles -->|Yes| Verify[Verify Context]
    Verify --> Strategy[Develop Strategy]
    Strategy --> Present[Present Approach]
```

### Act or Agent Mode
```mermaid
flowchart TD
    Start[Start] --> Context[Check Memory Bank]
    Context --> Update[Update Documentation]
    Update --> Execute[Execute Task]
    Execute --> Document[Document Changes]
    Execute --> Document[Document Changes]
```

## Documentation Updates
Memory Bank updates occur when:
1. Discovering new project patterns
2. After implementing significant changes
3. When user requests with **update memory bank** or **consume memory bank** (review all core files)
4. When context needs clarification
 
```mermaid

flowchart TD
    Start[Update Process]
    subgraph Process
        P1[Review Core Files]
        P2[Document Current State]
        P3[Clarify Next Steps]
        P1 --> P2 --> P3
    end
    Start --> Process
```
Note: When triggered by **update memory bank**, I MUST review every memory bank file, even if some don't require updates. Focus particularly on activeContext.md and progress.md as they track current state.

---

## Scope

**IMPORTANT:** Command Bank files are not to be included in the memory bank. The memory bank focuses on the project being worked.



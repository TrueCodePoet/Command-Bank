# Command: Journal Retrospective

## Command Acronyms: j-Retro

**Description**: Analyze recent git commit activity to extract emotional insights, workflow patterns, and improvement areas. Designed to help developers and teams continuously improve their process and mindset.

---

**Input Context:**
- No manual journal entry required. The command will review git commit history for the specified time range (default: last 7 days).
- You may specify a time window (e.g., "last week", "past 3 days") if desired.

---

**Instruction:**
1. **Always send a `cd` command to the project root folder as the very first step.** This ensures all subsequent git commands run in the correct directory.
2. Use git commands to gather commit messages, diffs, and activity for the given time range.
3. Provide the following in your output:
   - **Summary of key emotional tones and focus areas**
   - **Technical decision-making biases or blind spots**
   - **Suggested improvements to process or mindset** (prioritized, actionable)
   - **Concrete goals for the next development cycle**
4. Format your output in markdown, using clear headers and bullet points. Example structure:

   ```markdown
   ## Retrospective Summary
   - ...

   ## Technical Patterns & Biases
   - ...

   ## Actionable Improvements
   1. ...
   2. ...

   ## Goals for Next Cycle
   - ...
   ```
5. Optionally, prompt the user to specify a different time window for analysis.

---

**Recommended git commands (read-only):**
- `git log --since="7 days ago" --oneline --stat`
- `git diff <commit1> <commit2>`
- `git status`
- `git branch`

*Do not use git to write or commit any data; this is only for information gathering. Always run a single `cd` command to set the working directory before running git commands.*


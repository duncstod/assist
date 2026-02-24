---
description: Add a task to your task list.
allowed-tools: Read, Edit, AskUserQuestion
---

## Flow

1. If no argument provided, ask: "What's the task?"
2. Read ~/.claude/NOW.md, find max ID in TASKS table (or start at 1 if empty)
3. Ask type using AskUserQuestion:
   - header: "Type"
   - options: "work", "personal"
4. **If type is "work":** check ~/.claude/PROJECTS.md for active projects. If any exist, ask using AskUserQuestion:
   - header: "Project"
   - options: list active project slugs from ~/.claude/PROJECTS.md + "None"
   - Default to "None" if user skips or task clearly doesn't relate
5. Add row with ID+1 to TASKS table
6. Confirm: "Task added: [text]" (include project name if assigned)

## Details

- Get current date from context or system
- Insert new row at end of TASKS table, before the closing `---`
- Format: `| [ID] | [task text] | [type] | [project slug or --] | -- | -- | open |`
- Source and Due default to `--` (user can specify if relevant)
- Project = slug from ~/.claude/PROJECTS.md if selected, otherwise `--`

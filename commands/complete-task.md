---
description: Mark a task as complete.
allowed-tools: Read, Edit, AskUserQuestion
---

## Flow

1. Read ~/.claude/NOW.md TASKS section
2. If no open tasks: "No open tasks to complete."
3. If open tasks: Show numbered list of open tasks, ask which to complete
4. Change status of selected task(s) from `open` to `done`
5. Confirm: "Completed: [task text]"

## Details

- Support completing multiple tasks at once (e.g., "1 and 3" or "all open")
- Keep the table header row intact
- Mark as `done`, don't delete rows (preserves history)
- If completed task has a project slug, remind: "This is on [project]. Update with /project-status?"

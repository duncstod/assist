---
description: Show your current task list with filtering and status summary.
argument-hint: "[all|done|work|personal|overdue|project:slug]"
allowed-tools: Read, AskUserQuestion
---

## Flow

1. Read ~/.claude/NOW.md TASKS section
2. Parse the task table
3. Display tasks grouped by status, with optional filtering

## Default Display (no arguments)

Show open tasks only, grouped by project first, then unaffiliated:

```
OPEN TASKS (X of Y total)

[PROJECT NAME] (slug)
  [ID] [Task] (due: [date])
  ...

[OTHER PROJECT NAME] (slug)
  [ID] [Task] (due: [date])
  ...

UNAFFILIATED WORK
  [ID] [Task] (due: [date])
  ...

PERSONAL
  [ID] [Task] (due: [date])
  ...
```

- Group work tasks by project slug first (read ~/.claude/PROJECTS.md for project names)
- Tasks with project = `--` go under UNAFFILIATED WORK
- Omit due field if `--`
- Sort by due date first (soonest at top), then by ID within each group
- Flag overdue tasks: "[Task] -- OVERDUE (was [date])"
- Skip empty groups silently

## Arguments

- `all` -- show all tasks (open + done)
- `done` -- show only completed tasks
- `work` -- show only work tasks
- `personal` -- show only personal tasks
- `project:[slug]` -- show tasks for a specific project (e.g., `project:website-redesign`)
- `overdue` -- show only overdue open tasks

Arguments can be combined (e.g., `/list-tasks work overdue`).

## Summary Line

End with a one-line summary:

```
X open (Y work, Z personal) | N overdue | M completed
```

## Prompt

If there are overdue tasks: "Any of these done? Use `/complete-task` to clear them."
Otherwise: "Need to add one? `/add-task`"

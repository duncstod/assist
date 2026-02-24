---
description: Show all active projects with status summary.
allowed-tools: AskUserQuestion, Read
---

Read ~/.claude/PROJECTS.md, all project files in ~/.claude/projects/, and ~/.claude/NOW.md (for missions).

## Display

Show the ACTIVE table from ~/.claude/PROJECTS.md.

For each project, read its file (~/.claude/projects/{slug}.md) and add:
- Current focus
- Blockers (if any)
- Last LOG entry date

Format as:

```
ACTIVE PROJECTS

[Project Name] (slug)
  Status: [status] | Lead: [stakeholder]
  Focus: [current focus]
  Blockers: [if any, or "None"]
  Last update: [date of last LOG entry]

[Next project...]
```

## Highlight Issues

- Projects with blockers: Flag them
- Stale projects (no LOG entry in 7+ days): "[Project] hasn't been updated in [N] days"

## Connect to Missions

Reference ~/.claude/NOW.md Active Missions:

```
MISSION MAPPING

[MISSION 1]: [projects]
[MISSION 2]: [projects]
```

## Prompt

"Want to update one of these? Or `/add-project` to start a new one."

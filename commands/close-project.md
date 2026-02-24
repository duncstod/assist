---
description: Archive a completed or abandoned project. Capture lessons.
argument-hint: "[project-slug]"
allowed-tools: AskUserQuestion, Read, Write, Edit
---

Read ~/.claude/PROJECTS.md and the relevant project file (~/.claude/projects/{slug}.md).

## Select Project

If argument provided (e.g., `/close-project website-redesign`), use that slug directly.

Otherwise, use `AskUserQuestion`:
- header: "Project"
- question: "Which project are you closing?"
- options: Build from ~/.claude/PROJECTS.md ACTIVE table

## Ask Outcome

Use `AskUserQuestion`:
- header: "Outcome"
- question: "Is this done, or are you abandoning it?"
- options:
  - label: "Done"
    description: "Project completed successfully"
  - label: "Abandoning"
    description: "Stopping work, not completing"

## Capture Lesson

If Done:
"What worked? What would you do differently?"

If Abandoning:
"Why? What's the lesson?"

Wait for response.

## Update Project File

Add final LOG entry to ~/.claude/projects/{slug}.md:

```markdown
### [Today's date]
- **Closed:** [Done/Abandoned]
- **Lesson:** [Their response]
```

Update header status to "Closed":
`> Slug: [slug] | Created: [date] | Status: Closed`

## Update ~/.claude/PROJECTS.md

Remove from ACTIVE table.

Add to ARCHIVE table:
| [Name] | [slug] | [Today's date] | [One-line outcome: "Completed" or "Abandoned - reason"] |

Remove from CROSS-REFERENCES sections (Projects by Stakeholder and Projects by Mission).

Update "Last Updated" date.

## Close

"Archived [name]. [One observation about patterns if applicable - e.g., 'Third project abandoned due to scope creep. Pattern?']"

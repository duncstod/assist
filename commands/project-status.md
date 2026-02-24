---
description: Quick status update on a project. Surface blockers, track progress.
argument-hint: "[project-slug]"
allowed-tools: AskUserQuestion, Read, Write, Edit
---

Read ~/.claude/PROJECTS.md (for active projects), and the relevant project file (~/.claude/projects/{slug}.md).

## Select Project

If argument provided (e.g., `/project-status website-redesign`), use that slug directly.

Otherwise, use `AskUserQuestion`:
- header: "Project"
- question: "Which project?"
- options: Build from ~/.claude/PROJECTS.md ACTIVE table (label: project name, description: current status)

## Display Current State

Read the project file (~/.claude/projects/{slug}.md) and show:
- Status
- Current focus
- Blockers (if any)
- Next step

Keep it brief - just the key info.

## Ask

"What's the update?"

Wait for response. Could be:
- Progress made
- Blocker hit
- Decision made
- Question to think through

## Update Project File

Based on their answer:

### If progress
- Add to LOG with today's date
- Update "Focus" if changed
- Update "Next" with their next step

### If blocker
- Add to LOG
- Update "Blockers" field
- Change Status to "Blocked" in header if significant
- Update ~/.claude/PROJECTS.md Status column if changed

### If decision
- Add to LOG with decision and rationale

### If question
- Suggest: "Want to use /project-think to work through this?"

## Pattern Check

If same blocker mentioned in LOG 3+ times:
"This is the third time [blocker] has come up. Time to escalate or rethink?"

## Close

"Updated."

Or if blocker: "Updated. [Blocker] logged. Who can help unblock this?"

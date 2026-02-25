---
description: Prepare for an upcoming meeting. Builds talking points, anticipated questions, and perspectives.
allowed-tools: AskUserQuestion, Read, Write, Edit, mcp__google-calendar__list-events, mcp__google-calendar__get-current-time
---

Read ~/.claude/ASSIST.md (for stakeholder profiles), ~/.claude/COACH.md (for personality), ~/.claude/MEETING.md (for meeting state), and ~/.claude/PROJECTS.md (for project context).

## Context

First, get current time and fetch upcoming calendar events:

1. Call `mcp__google-calendar__get-current-time` to get today's date/time (if available, otherwise use `date`)
2. Call `mcp__google-calendar__list-events` with:
   - calendarId: "primary"
   - timeMin: current time
   - timeMax: 7 days from now
   - fields: ["summary", "start", "end", "attendees", "description"]

If calendar MCP is not available, skip to asking which meeting they're prepping for.

Read silently: ~/.claude/ASSIST.md (stakeholders), ~/.claude/COACH.md (personality), ~/.claude/MEETING.md (current state).

## Select Meeting

Use `AskUserQuestion` to present upcoming meetings:

- header: "Meeting"
- question: "Which meeting are you prepping for?"
- multiSelect: false
- options: Build from calendar events (up to 4):
  - label: "[Meeting title] - [Day] [Time]"
  - description: "With: [attendee names]" (or "No attendees listed" if none)

Sort by start time (soonest first). If more than 4 meetings, show the next 4 - user can select "Other" and type a meeting name.

If no calendar events found, fall back to asking: "Which meeting are you prepping for?" as free text.

## After Selection

Parse the selected meeting. If they selected from calendar, extract attendee info automatically.

If they mention a person in their selection, check ~/.claude/ASSIST.md for their stakeholder profile.

Check ~/.claude/PROJECTS.md for projects involving any meeting attendees. If found, note them for later.

## Gather Context

Ask one at a time:

1. "What's the purpose of this meeting?"
2. "What do you need from this person?"
3. "What might they ask you about?"
4. "Is there anything you're nervous about?"

## Build Prep

Update ~/.claude/MEETING.md CURRENT PREP section with:

```markdown
## Meeting: [Name]
**With:** [Stakeholder]
**Date:** [Date/Time]
**Context:** [Why this meeting matters - from their answers]

### My Talking Points
- [Based on what they need from the meeting]
- [Based on stakeholder priorities from ASSIST.md]

### Questions to Ask
- [Based on what they want to learn/achieve]

### Anticipated Questions (+ my answers)
| They might ask | My answer |
|----------------|-----------|
| [From their nervous-about answer] | [Help them prepare answer] |

### Perspective to Have Ready
> [Their opinion/position on key topics - challenge if vague]

### Relevant Projects (if any)
| Project | Status | Recent Update |
|---------|--------|---------------|
| [From PROJECTS.md - projects where attendee is stakeholder] | [Status] | [Last LOG entry summary] |
```

Reference stakeholder profile from ~/.claude/ASSIST.md for context on what that person cares about.

If relevant projects exist, suggest project-related talking points:
- "[Attendee] is stakeholder on [project]. Update them on [current focus]."

### Pre-Meeting Checklist

If any prep involves project work:
- Reference the project file's (~/.claude/projects/{slug}.md) remaining steps
- Only add meeting-specific prep items directly (e.g., "rehearse narrative," "prepare slides")
- Do NOT copy project tasks into the checklist -- they are tracked in project files and ~/.claude/NOW.md TASKS

Also check ~/.claude/NOW.md TASKS for overdue or relevant tasks tied to meeting attendees or their projects.

## Challenge

Apply the decision test from ~/.claude/COACH.md:
- "Is this meeting about visibility, or could you handle this async?"
- "What's the one thing you need them to walk away knowing?"

If their talking points are vague, push back: "That's generic. What specifically?"

## Close

"You're prepped. One thing to nail: [their key point]"

Update UPCOMING table in ~/.claude/MEETING.md with prep status = "Ready"

---
description: Morning kickoff. Sets intentions and MIT for the day.
allowed-tools: AskUserQuestion, Read, Write, Edit, mcp__google-calendar__get-current-time, mcp__google-calendar__list-events
---

Read ~/.claude/ASSIST.md, ~/.claude/COACH.md, ~/.claude/NOW.md, ~/.claude/MEETING.md and ~/.claude/PROJECTS.md for full context.

## Context

Get current time via MCP tool `get-current-time` (if Google Calendar MCP is available). Otherwise, run: `date '+%A %B %d, %Y %H:%M'`

Fetch today's calendar events via MCP tool `list-events` (calendarId: "primary", timeMin: today start, timeMax: today end). If calendar MCP is not available, skip silently.

Read silently: ~/.claude/ASSIST.md (context), ~/.claude/COACH.md (personality), ~/.claude/NOW.md (current state), ~/.claude/MEETING.md (prep status), ~/.claude/PROJECTS.md (active projects).

## Check for Missed Sessions

Read ~/.claude/NOW.md Memory Log - find the most recent entry.

Parse the date and time marker (AM/PM) from the header (format: `### YYYY-MM-DD (AM|PM)`).

**If last entry was AM (missed end-day):**
- "Looks like you started [date] but didn't close out. Quick summary?"
- Wait for response
- Add brief PM Memory Log entry for that date with their summary
- Continue with today's start-day

**If last entry was PM but more than 1 day ago:**
- Note: "Welcome back. [X] days since last check-in."
- Continue normally

**If last entry was PM from yesterday:**
- Continue normally

## Check Meetings

If there are meetings today (from calendar or ~/.claude/MEETING.md UPCOMING):
1. Check ~/.claude/MEETING.md CURRENT PREP section
2. If any meeting is today and CURRENT PREP is empty or for a different meeting:
   - "You have **[meeting name]** at [time]. No prep done. Want to `/assist::prep-meeting` first?"
   - Wait for response before continuing

## Surface Tasks

If ~/.claude/NOW.md TASKS table has open entries:
- Show overdue tasks (due date has passed) first, flagged
- Show tasks due today
- Briefly list other open tasks (group by project if helpful)
- "Open tasks: [list]. Any of these done or no longer needed?"
- If any done -> mark status as `done` in TASKS table
- Continue to priorities (don't block on this)

### Stale Task Check

After surfacing open tasks, scan for stale tasks:
- **Stale = open task with no due date AND sourced more than 14 days ago**
- If stale tasks found, flag them briefly: "Stale (2+ weeks, no due date): [task IDs + short names]. Still alive or should we close them?"
- Wait for response. Mark any they want closed as `done`.
- Don't block on this -- keep it quick.

## Project Backlog Check

After tasks are surfaced, check active project backlogs:

1. Read ~/.claude/PROJECTS.md for active projects
2. For each active project, read the project file's (~/.claude/projects/{slug}.md) "Remaining Steps" section
3. Count unchecked items (lines starting with `- [ ]`)
4. If any project has unchecked items, show a brief summary:
   - "[project name]: [N] unchecked items in backlog"
   - List the first 3 unchecked items as examples
5. This is awareness only -- don't ask to pull items into TASKS. The user's priority-setting handles that.
6. Skip projects with 0 unchecked items silently.

## Ask

"What are your top 3 priorities today?"

That's it. Wait.

## After they answer

**If they list more than 3:**
- "That's more than 3. Which ones are you actually doing today?"
- Wait for them to narrow down

**If 3 or fewer:**
1. Update ~/.claude/NOW.md:
   - Clear QUEUE section
   - Add numbered priorities (1-3) to QUEUE
   - Set MIT Today = their #1 priority
   - Add Memory Log entry if pattern observed
2. Confirm: "Got it. Your queue: [list]. #1 is your MIT."

## Connect (if appropriate)

If ~/.claude/COACH.md has a mission or deadline, connect briefly:
- "That moves you toward [their mission]."
- "[X] days to [deadline]."

If MIT connects to an active project in ~/.claude/PROJECTS.md:
- "That's on [project name]."
- If project has blocker: "Still blocked on [blocker]. Addressing today?"

## Close

Short:
- "Three things. Go."
- "[X] days left. Back to it."

## Observe (don't output)

Notice:
- Energy in their words
- Hesitation
- Same priorities as yesterday?
- Avoiding something?

If pattern (3x+), add to Memory Log and mention: "This is the third time you've set this. What's in the way?"

## Memory Log Entry

Every /start-day should add a Memory Log entry in ~/.claude/NOW.md:

```markdown
### YYYY-MM-DD (AM)
- Queue: [their 3 priorities]
- MIT: [#1 priority]
- [Any pattern or observation worth noting]
```

The (AM) marker indicates start-day was run. This enables /end-day to detect missed sessions.

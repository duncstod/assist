---
description: Evening review. Captures wins, lessons, and prep for tomorrow.
---

Read ~/.claude/CLAUDE.md, ~/.claude/COACH.md, ~/.claude/NOW.md, ~/.claude/MEETING.md, and ~/.claude/PROJECTS.md for full context.

## Context

Run: `date '+%A %B %d, %Y %H:%M'`

If before 6pm: "Closing out early?"

Read silently: ~/.claude/CLAUDE.md (context), ~/.claude/COACH.md (personality), ~/.claude/NOW.md (current state), ~/.claude/MEETING.md (check for past meetings), ~/.claude/PROJECTS.md (active projects).

## Check for Missed Sessions

Read ~/.claude/NOW.md:
1. Check QUEUE section - is it empty/default?
2. Check Memory Log - find the most recent entry

**If QUEUE is empty AND last entry was PM (missed start-day):**
- "Looks like you didn't start today. What did you work on?"
- Wait for response
- Capture their answer as today's priorities (retroactive)
- Continue with normal end-day reflection

**If last entry was AM from today:**
- Continue normally (start-day was run)

**If multi-day gap:**
- "Been a few days. Let's catch up on today."
- Continue with normal flow

## Ask

"How'd it go?"

Let them talk. Don't ask 5 questions.

## Follow up (maybe)

One question if needed:
- "Did you get through your queue?"
- "What got in the way?"
- "Anything carrying to tomorrow?"

Or nothing.

## Update

**Update ~/.claude/NOW.md:**
- Add Memory Log entry with today's observation
- Quote important words: *'their exact words'*
- Note patterns, wins, or blocks
- Update TASKS table: mark completed items as `done`, add new tasks from today's work
- If completed/updated tasks have a project slug, also update the project file (~/.claude/projects/{slug}.md) LOG

**Update ~/.claude/COACH.md only if:**
- New long-term pattern discovered (add to Bugs)
- Mission changed (rare)

**Update project files (~/.claude/projects/{slug}.md) if:**
- They mention progress on an active project -> add to project LOG
- They mention a blocker on a project -> add to project Current State > Blockers
- They mention a decision -> add to project LOG

## Clean up ~/.claude/MEETING.md

Check ~/.claude/MEETING.md UPCOMING table:
1. Look for meetings with dates before today
2. For each past meeting:
   - Check if there's a matching LOG entry
   - If no LOG entry: "Looks like **[meeting name]** happened but wasn't reviewed. Quick summary?"
   - If they provide one, add a brief LOG entry
   - Remove the past meeting from UPCOMING table
3. If UPCOMING is now empty, leave as empty table (keeps structure)

## Observe and maybe surface

If pattern (3x+):
- "You've mentioned [X] a few times. Worth naming?"
- "That's the third day you [pattern]. What's going on?"
- **Add to Memory Log**

If they hit MIT multiple days:
- "That's [N] days in a row. What's working?"
- **Add to Memory Log**

If they missed MIT:
- "What got in the way?" - no guilt
- **Add to Memory Log**

## Close

Short:
- "Rest."
- "Tomorrow: [their next thing if set]"
- Connect to mission if deep enough

## Memory Log Entry

Every /end-day should add a Memory Log entry in ~/.claude/NOW.md:

```markdown
### YYYY-MM-DD (PM)
- [Key observation from today]
- [Pattern if noticed]
- Quote: *'their exact words if important'*
```

The (PM) marker indicates end-day was run. This enables /start-day to detect missed sessions.

This is the core feature. The log builds pattern recognition over time.

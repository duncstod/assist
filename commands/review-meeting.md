---
description: Post-meeting reflection. Captures what worked, what didn't, and lessons.
---

Read ~/.claude/ASSIST.md (for stakeholders), ~/.claude/COACH.md (for personality), and ~/.claude/MEETING.md for context.

## Context

Run: `date '+%A %B %d, %Y %H:%M'`

Read silently: ~/.claude/ASSIST.md (stakeholders), ~/.claude/COACH.md (personality), ~/.claude/MEETING.md (check CURRENT PREP for what they prepped).

## Ask

"How'd it go?"

Let them talk. Don't ask 5 questions.

## Follow up (maybe)

One question if needed:
- "Did you land your main point?"
- "Anything you fumbled?"
- "What do they think of you now?"

Or nothing.

## Update ~/.claude/MEETING.md

Move CURRENT PREP content to LOG as Meeting History entry:

```markdown
### [Date] - [Meeting name] with [Person]
- **Went well:** [What worked - from their words]
- **Fumbled:** [What didn't work - quote their words if strong]
- **Follow-up:** [Action items they mentioned]
- **Lesson:** [What to do differently next time]
```

Clear CURRENT PREP section back to default:
```markdown
*No meeting currently being prepped. Run `/assist::prep-meeting` to start.*
```

Remove meeting from UPCOMING table (if it exists there).

## Update ~/.claude/NOW.md TASKS (if follow-ups)

If follow-ups were captured:
1. Show the list: "Follow-ups: [list]"
2. Add each as a new row in ~/.claude/NOW.md TASKS table:
   - Find max ID in TASKS table, increment for each new task
   - Set Source = "[Meeting name] [date]"
   - Set Project = project slug if follow-up relates to an active project (check ~/.claude/PROJECTS.md)
   - Set Type = "work"
   - Set Status = "open"
   - Set Due = date if mentioned, otherwise "--"
3. Confirm: "Added [N] tasks from this meeting."

## Update ~/.claude/ASSIST.md (if needed)

If new insight about the stakeholder:
- Update their profile in STAKEHOLDERS section
- E.g., "Prefers data first, then context" or "Gets impatient with long explanations"

## Observe and maybe surface

If pattern (3x+):
- "You've fumbled [X] type of question a few times. Worth prepping differently?"
- Add to Memory Log

If they nailed it:
- "That's [N] good meetings in a row with [person]. What's working?"

## Close

"Noted. [One observation about pattern if applicable]"

Or just: "Logged."

---
description: Show upcoming meetings. Calendar-aware if MCP connected.
---

Read ~/.claude/MEETING.md for current state.

## Check Calendar (if MCP connected)

If Google Calendar MCP is available:
- Fetch upcoming meetings for next 7 days
- Display in table format
- Cross-reference with ~/.claude/MEETING.md UPCOMING table for prep status

## Display

Show upcoming meetings:

| Meeting | With | Date | Prep Status |
|---------|------|------|-------------|
| [from calendar or MEETING.md] | | | |

Highlight any without prep:
- "You have [meeting] with [person] on [date] - not prepped yet."

## If No Calendar MCP

"Calendar not connected. Here's what's in MEETING.md:"

[Show UPCOMING table from ~/.claude/MEETING.md]

"To add a meeting, tell me about it and I'll add it to the list."

If they describe a meeting, add it to UPCOMING table in ~/.claude/MEETING.md.

## Prompt

If meetings coming up soon without prep:
- "Want to prep for [nearest unprepped meeting] now?"

## Calendar Setup Note

To connect Google Calendar:
1. Set up Google Calendar MCP server
2. Add to Claude Code MCP settings
3. `/list-meetings` will then pull live calendar data

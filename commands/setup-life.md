---
description: First-time setup. Creates context files (ASSIST.md or CLAUDE.md), COACH.md, NOW.md, and MEETING.md through a 5-minute conversation.
---

# Setup Life

You're setting up a new user's 4-file system:
- **ASSIST.md** (or **CLAUDE.md** -- user's choice) -- Generic context (loads every session)
- **COACH.md** -- Coaching personality (loaded by assistant commands)
- **NOW.md** -- Life assistant state
- **MEETING.md** -- Meeting assistant state

This is one-time onboarding.

Ensure the ~/.claude/projects/ directory exists before creating any files.

## Your approach

Be warm but efficient. This isn't therapy -- it's setup. Get the essential info to make the system work.

Ask ONE question at a time. Wait for their answer before asking the next.

## The conversation

### 1. Welcome

"Let's set up your system. I'll ask a few questions to understand how to help you.

First -- what should I call you?"

*Wait for answer.*

### 1b. Context file

"One quick setup question. This plugin stores your identity, stakeholders, and preferences in a context file. You have two options:

- **CLAUDE.md** -- Your context loads in every Claude Code session, even outside /assist:: commands. Best if you want your identity always available.
- **ASSIST.md** -- Separate file just for this plugin. Keeps your CLAUDE.md untouched. Best if you already have your own CLAUDE.md."

*Wait for answer. Remember their choice for the file creation step.*

### 2. Basic info

"How old are you and where are you based? (Include timezone if you know it)"

*Wait for answer.*

### 3. Role

"What do you do? What's your job/role and what tools or skills do you use?"

*Wait for answer.*

### 4. Communication

"Any communication preferences I should know? (e.g., Slack vs email, direct vs gentle)"

*Wait for answer.*

### 5. Mission

"What are you working toward right now? Could be a goal, a project, a life change -- whatever's top of mind."

*Wait for answer.*

### 6. Deadline

"Is there a deadline or timeframe for this?"

*Wait for answer. If no deadline, ask: "When would you want to see progress by?"*

### 7. Patterns

"What usually gets in your way? What patterns trip you up?"

*Wait for answer.*

### 8. Challenge style

"When you're off track, how should I call you out? Direct and blunt? Gentle questions? Something else?"

*Wait for answer.*

### 9. Modes

"What modes do you operate in? For example:
- BUILDER (shipping code) vs BROWSER (procrastinating)
- STRATEGIST (planning) vs EXECUTOR (doing)
- HUMAN (rest and recovery)

What are 2-3 modes that describe how you work?"

*Wait for answer.*

### 10. Active missions

"What are your active missions right now? (2-3 max, things you're actively working on)"

*Wait for answer.*

### 11. Key stakeholders

"Who are the key people you work with? (Managers, colleagues, clients -- people you need to influence or impress)"

*Wait for answer.*

---

## Create context file

The user chose either CLAUDE.md or ASSIST.md in step 1b. Follow the matching path.

### If user chose CLAUDE.md:

1. Check if `~/.claude/CLAUDE.md` already exists and has content.
2. **If it exists with content:**
   - Tell the user: "You already have a CLAUDE.md. I'll add the Assist sections to it. Your existing content stays."
   - Read its contents. Append the sections below (ME, STAKEHOLDERS, ASSISTANT FILES) to the end of the existing file under an `---` separator. Skip any sections that already exist.
3. **If no existing CLAUDE.md:** Create it fresh with the template below, using the heading `# CLAUDE.md -- [Name]` and description `> Personal context for Claude Code sessions.`
4. **Create symlink:** If `~/.claude/ASSIST.md` already exists as a real file, back it up to `~/.claude/ASSIST.md.backup`. Then run: `ln -sf ~/.claude/CLAUDE.md ~/.claude/ASSIST.md`

### If user chose ASSIST.md:

1. If `~/.claude/ASSIST.md` already exists (re-running setup):
   - If it's a symlink, tell the user: "You previously chose CLAUDE.md mode. Switching to standalone ASSIST.md." Remove the symlink.
   - If it's a real file, ask: "You already have an ASSIST.md. Start fresh or keep existing?"
2. Create `~/.claude/ASSIST.md` with the template below, using the heading `# ASSIST.md -- [Name]` and description `> Personal context for the Assist plugin.`
3. Do not touch `~/.claude/CLAUDE.md`.

### Template (used by both paths):

Use the heading and description matching their choice (see above).

```markdown
# [HEADING -- see above]

> [DESCRIPTION -- see above]

---

# ME

## Identity
- **Name:** [Name]
- **Age:** [Age]
- **Location:** [City, Country (Timezone)]

## Role
[Their job/role from conversation]
- **Focus areas:** [What they work on]
- **Stack:** [Tools, skills, technologies]

## Preferences
- [Communication preferences from conversation]
- Be direct and concise
- No emojis unless asked

---

# STAKEHOLDERS

## [Stakeholder 1 Name]
- **Role:** [Their role]
- **Priorities:** [What they care about - infer or ask later]
- **Communication style:** [How to engage - infer or ask later]
- **Your history:** [To be filled in]
- **Prep focus:** [To be filled in]

[Repeat for each key stakeholder mentioned]

---

# ASSISTANT FILES

| File | Purpose | When to Read |
|------|---------|--------------|
| `NOW.md` | Current priorities, active tasks, working mode, memory log | What am I working on? My tasks? Priorities? Recent context? |
| `PROJECTS.md` | Active project index with stakeholders and status | Any question about projects |
| `projects/{slug}.md` | Detailed project state: goals, remaining steps, log | Discussing a specific project (get slug from PROJECTS.md) |
| `MEETING.md` | Meeting prep, upcoming meetings, meeting history | Meetings, prep, or follow-ups |
| `COACH.md` | Coaching personality | Only loaded by coaching commands (/assist::start-day, /assist::end-day, etc.) |
```

---

## Create ~/.claude/COACH.md (if it doesn't exist)

Create ~/.claude/COACH.md with this structure (coaching personality):

```markdown
# COACH.md -- Life + Meeting Assistant

> Coaching personality. Only loaded by /assist::start-day, /assist::check-day, /assist::end-day, /assist::prep-meeting, /assist::review-meeting.

---

# AGENT

## Identity
Personal coach living in this filesystem. Grows with [Name] over time.

## Personality
- **Direct** -- No coddling, no generic advice
- **Challenger** -- Quote words back when off track
- **Pragmatic** -- Ship over perfect, action over planning

## Rules
- Concise (1-4 sentences when possible)
- Reference deadlines for urgency
- Key question: *"[Customize based on their patterns - see examples below]"*

---

# [NAME]'S PSYCHOLOGY

## Mission

> "[Their mission in their exact words]"

[Break into 1-2 specific statements]

## Drivers
[Infer from conversation - what motivates them]

## Bugs
1. [Pattern 1 from their words]
2. [Pattern 2 from their words]

## What Works
[Their preferred challenge style]

---

# HOW WE WORK

1. Read `ASSIST.md` (context) + `COACH.md` (personality) + `NOW.md` or `MEETING.md` (state). Note: if the user chose CLAUDE.md, write `CLAUDE.md` instead of `ASSIST.md` here.
2. Challenge, mirror, assist during session
3. Update state files when something meaningful happens

## Decision Test
- Does this move toward [their mission]?
- [Add 1-2 more questions based on their context]

---

*See `NOW.md` for life state, `MEETING.md` for meeting state.*
```

**Key question examples (customize based on their bugs):**
- Building to avoid launching? -> *"Are you building to avoid launching?"*
- Perfectionism? -> *"Is 'not good enough' protecting you from being judged?"*
- Avoiding rejection? -> *"Are you avoiding rejection by not putting yourself out there?"*
- Tutorial hell? -> *"Are you learning, or are you preparing to learn?"*
- Generic default -> *"Is this what you actually want, or what you think you should want?"*

---

## Create ~/.claude/NOW.md

Create ~/.claude/NOW.md with this structure:

```markdown
# NOW.md -- Current State

> Dynamic file. Update often. See `COACH.md` for mission and psychology.

**Last Updated:** [Today's date]

---

# QUEUE

> Live tasks. Updated during sessions.

- (empty)

---

# TASKS

| ID | Task | Type | Project | Source | Due | Status |
|----|------|------|---------|--------|-----|--------|

---

# MODE

## Current: [Their default mode from conversation]

| Mode | Focus | Not Allowed |
|------|-------|-------------|
| [MODE1] | [Their description] | [What they avoid] |
| [MODE2] | [Their description] | [What they avoid] |
| [MODE3] | [Their description] | [What they avoid] |

*Say "switching to [mode]" to change*

---

# THIS WEEK

## Active Missions
1. **[MISSION 1]** -- [One-line description from conversation]
2. **[MISSION 2]** -- [One-line description from conversation]

## Actions

| Action | Deadline | Status |
|--------|----------|--------|
| [Infer from mission] | [Their deadline] | open |

**MIT Today:** [Leave blank - will set next]

## Bucket (For Later)

- [ ] [Backlog item]

---

# LOG

## Memory (AI Notes)

### [Today's date]
- System initialized. [Name] is working on [missions]. Deadline: [their deadline].
- Known bugs: [list their patterns]
- Challenge style: [their preference]

---

*Mode at end of day: [Their current mode]*
```

---

## Create ~/.claude/MEETING.md

Create ~/.claude/MEETING.md with this structure:

```markdown
# MEETING.md - Meeting Prep State

> Dynamic file. See `ASSIST.md` for stakeholder profiles. Note: if the user chose CLAUDE.md, write `CLAUDE.md` instead of `ASSIST.md` here.

**Last Updated:** [Today's date]

---

# UPCOMING

| Meeting | With | Date | Prep Status |
|---------|------|------|-------------|
| (none scheduled) | - | - | - |

---

# CURRENT PREP

*No meeting currently being prepped. Run `/assist::prep-meeting` to start.*

---

# LOG

## Meeting History

*No meetings logged yet. Run `/assist::review-meeting` after a meeting to capture learnings.*

---

*Use `/assist::prep-meeting` to prepare, `/assist::review-meeting` to reflect, `/assist::list-meetings` to see upcoming.*
```

---

## Also create ~/.claude/PROJECTS.md

Create ~/.claude/PROJECTS.md with this structure:

```markdown
# PROJECTS.md - Project Index

> Central registry. See `projects/` for details.

**Last Updated:** [Today's date]

---

# ACTIVE

| Project | Slug | Lead Stakeholder | Status | Priority |
|---------|------|------------------|--------|----------|

---

# ARCHIVE

| Project | Slug | Closed | Outcome |
|---------|------|--------|---------|

---

# CROSS-REFERENCES

## Projects by Stakeholder

## Projects by Mission

---

*Use `/assist::add-project` to create, `/assist::project-status` to update, `/assist::close-project` to archive.*
```

---

## Close

"You're set up. I've created five files:
- **[ASSIST.md or CLAUDE.md]** -- Your basic context (loads every session). Use the filename matching their choice.
- **COACH.md** -- Coaching personality (activates with assistant commands)
- **NOW.md** -- Your current state, updated daily
- **MEETING.md** -- Meeting prep and history
- **PROJECTS.md** -- Project index

If they chose CLAUDE.md, add: "Since you chose CLAUDE.md, your identity and stakeholders will be available in all Claude Code sessions -- not just /assist:: commands."

Here's how it works:
- `/assist::start-day` -- Morning. Set your priorities.
- `/assist::check-day` -- Anytime. Quick check-in.
- `/assist::end-day` -- Evening. Capture what happened.
- `/assist::prep-meeting` -- Prepare for a meeting.
- `/assist::review-meeting` -- Reflect after a meeting.
- `/assist::add-stakeholder` -- Add a new stakeholder profile.
- `/assist::add-project` -- Start tracking a new project.

The Memory Log in NOW.md will track patterns over time. The longer you use it, the better it gets.

What's your one thing for today?"

*If they answer, update ~/.claude/NOW.md with their MIT. Add a Memory Log entry: "First MIT set: [their thing]"*

---
description: Create a new project with goals, stakeholders, and mission connection.
allowed-tools: AskUserQuestion, Read, Write, Edit
---

Read ~/.claude/ASSIST.md (for stakeholder profiles), ~/.claude/NOW.md (for active missions), ~/.claude/PROJECTS.md (for existing projects).

## Ask

"What project are you starting?"

Wait for name.

## Gather Info

Ask one at a time:

1. "What's the goal? One sentence - what does done look like?"
2. "Why does this matter? (Visibility, impact, stakeholder need?)"
3. "Who are the key stakeholders?" (Reference ~/.claude/ASSIST.md profiles if relevant)
4. "Which mission does this connect to?" (Reference ~/.claude/NOW.md Active Missions)

## Challenge

Apply decision test from ~/.claude/COACH.md:
- "Is this high-impact or just technically interesting?"
- If it doesn't connect to a mission or stakeholder: "This feels disconnected. How does it tie to your goals?"

## Create Project File

Generate slug from name (lowercase, hyphens: "Website Redesign" -> "website-redesign")

Create ~/.claude/projects/{slug}.md with:

```markdown
# PROJECT: [Name]

> Slug: [slug] | Created: [Today's date] | Status: Planning

---

## Goal
[Their answer to Q1]

## Why It Matters
[Their answer to Q2]

## Stakeholders
[Their answer to Q3 - format as: Person (Role) | Person (Role)]

---

## Current State

**Focus:** [Starting - define first step]
**Blockers:**
**Next:** [To be defined]

---

## LOG

### [Today's date]
- Project created

---

*Mission: [Their answer to Q4]*
```

## Update ~/.claude/PROJECTS.md

Add to ACTIVE table:
| [Name] | [slug] | [Lead stakeholder from their answer] | Planning | P2 |

Add to CROSS-REFERENCES:
- Under "Projects by Stakeholder" - add project to each stakeholder mentioned
- Under "Projects by Mission" - add project to the mission

Update "Last Updated" date.

## Close

"Created [name]. Slug: [slug]. Connected to [mission] via [stakeholder].

What's your first step?"

Log their answer as the "Next" in Current State.

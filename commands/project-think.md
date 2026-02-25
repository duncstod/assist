---
description: Think through a project decision, blocker, or strategic question.
argument-hint: "[project-slug]"
allowed-tools: AskUserQuestion, Read, Write, Edit
---

Read ~/.claude/projects/{slug}.md (project file), ~/.claude/ASSIST.md (for stakeholder context), ~/.claude/COACH.md (for challenge patterns and decision tests).

## Select Project

If argument provided (e.g., `/project-think website-redesign`), use that slug directly.

Otherwise, use `AskUserQuestion`:
- header: "Project"
- question: "Which project?"
- options: Build from ~/.claude/PROJECTS.md ACTIVE table

## Ask

"What do you need to think through?"

Wait for response. Identify category:
- Technical approach
- Stakeholder alignment
- Prioritization
- Strategic decision

## Facilitate Thinking

Based on category, ask probing questions. One at a time. Let them think.

### Technical approach
- "What are the options?"
- "What are the trade-offs of each?"
- "What's the simplest version that could work?"
- "What would you recommend to someone else in this situation?"

### Stakeholder alignment
Reference the stakeholder's profile from ~/.claude/ASSIST.md:
- "What does [stakeholder] actually need from this?"
- "What would make them say 'this is exactly what I wanted'?"
- "Where might your goals and theirs diverge?"
- "What's their communication style? How should you present this?"

### Prioritization
- "If you could only deliver one thing, what would it be?"
- "What's blocking the highest-impact work?"
- "Are you doing the necessary but unglamorous work, or chasing what's interesting?"

### Strategic decision
- "What are you actually deciding between?"
- "What information would make this obvious?"
- "What would [relevant stakeholder] say?"

## Challenge

Apply ~/.claude/COACH.md decision tests:
- "Is this technically interesting, or high-impact?"
- "Are you building influence, or just building models?"

If they're rationalizing, quote their words back: "You said '[their words]'. Is that the real reason?"

## Capture

If a decision is made:
- Add to project LOG (~/.claude/projects/{slug}.md): "[Date] - Decision: [summary]. Rationale: [why]."

If an insight emerges:
- Add to project LOG (~/.claude/projects/{slug}.md): "[Date] - Insight: [what was learned]"

## Close

If decision made:
"Decision: [summary]. Next action: [what they committed to]."

If still open:
"Still open. Park it and revisit [suggest timeframe]?"

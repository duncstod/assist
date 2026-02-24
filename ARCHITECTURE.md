# Architecture

## Overview

Assist is a personal productivity framework for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). It provides daily workflow commands (morning kickoff, meeting prep, project tracking) backed by persistent context files that maintain state across sessions.

Distributed as a **Claude Code plugin** via marketplace (`/plugin marketplace add duncstod/assist`). Commands live in `commands/` and are automatically discovered by Claude Code when the plugin is installed. State files live at `~/.claude/` and are created by `/setup-life`.

## Directory Layout

### Plugin structure (this repo)

```
├── .claude-plugin/
│   ├── plugin.json        # Plugin manifest
│   └── marketplace.json   # Marketplace manifest
├── commands/               # Command definitions (one file per command)
│   ├── start-day.md
│   ├── end-day.md
│   ├── check-day.md
│   ├── prep-meeting.md
│   ├── review-meeting.md
│   ├── list-meetings.md
│   ├── add-project.md
│   ├── project-status.md
│   ├── project-think.md
│   ├── list-projects.md
│   ├── close-project.md
│   ├── add-task.md
│   ├── complete-task.md
│   ├── list-tasks.md
│   ├── setup-life.md
│   └── add-stakeholder.md
├── templates/              # Reference templates for state files
│   ├── CLAUDE.md
│   ├── COACH.md
│   ├── NOW.md
│   ├── MEETING.md
│   ├── PROJECTS.md
│   └── projects/
│       └── example-project.md
├── README.md
├── ARCHITECTURE.md         # This file
├── LICENSE
└── LINKEDIN-POST.md
```

### User's `~/.claude/` (after `/setup-life`)

```
├── CLAUDE.md          # Personal context (identity, stakeholders)
├── COACH.md           # Coaching personality
├── NOW.md             # Daily state (priorities, tasks, memory log)
├── MEETING.md         # Meeting prep and history
├── PROJECTS.md        # Project index
├── projects/          # Individual project files
│   └── {slug}.md
├── mcp.json           # MCP server config (NOT from plugin)
├── settings.json      # Claude Code settings (NOT from plugin)
└── memory/            # Auto-memory (NOT from plugin)
```

## Core Files

| File | Purpose | Updated by |
|------|---------|------------|
| `CLAUDE.md` | Identity, stakeholders, assistant file index. Loaded in every session. | `/setup-life`, `/add-stakeholder`, manual edits |
| `COACH.md` | Coaching personality and tone. Read by daily workflow commands. | `/setup-life`, manual edits |
| `NOW.md` | Current priorities, MIT, active tasks, working mode, memory log. | `/start-day`, `/check-day`, `/end-day` |
| `MEETING.md` | Upcoming meetings, prep notes, meeting history. | `/prep-meeting`, `/review-meeting`, `/list-meetings` |
| `PROJECTS.md` | Index of active projects with status, stakeholders, slug. | `/add-project`, `/close-project`, `/project-status` |
| `projects/{slug}.md` | Detailed project state: goals, remaining steps, decision log. | `/project-status`, `/project-think` |

## How Shared Context Works

The system's power comes from **shared context across all commands**. Every command reads the same files:

```
CLAUDE.md --- identity + stakeholders ---+
COACH.md ---- personality + patterns ----+
NOW.md ------ priorities + tasks --------+-- Every command has full context
MEETING.md -- meeting state -------------+
PROJECTS.md -- project index ------------+
```

When you prep a meeting, the system already knows:
- Who the attendee is and what they care about (from CLAUDE.md)
- What projects involve them (from PROJECTS.md)
- What you're currently focused on (from NOW.md)
- Your patterns and blind spots (from COACH.md)

This is what makes it feel like an assistant rather than a chatbot.

## Commands

Each command lives in `commands/<name>.md` with YAML frontmatter (`description:`, optional `allowed-tools:`, optional `argument-hint:`).

### Command categories

| Category | Commands | Purpose |
|----------|---------|---------|
| **Daily** | `start-day`, `check-day`, `end-day` | Morning kickoff, midday check-in, evening review |
| **Meetings** | `prep-meeting`, `review-meeting`, `list-meetings` | Before, after, and overview |
| **Projects** | `add-project`, `project-status`, `project-think`, `list-projects`, `close-project` | Full project lifecycle |
| **Tasks** | `add-task`, `complete-task`, `list-tasks` | Simple task tracking in NOW.md |
| **Setup** | `setup-life`, `add-stakeholder` | Initial setup and stakeholder profiles |

### The Daily Loop

```
/start-day (AM)
    +-- Check for missed sessions
    +-- Surface today's meetings
    +-- Surface open/overdue tasks
    +-- Check project backlogs
    +-- Set 3 priorities + MIT
    +-- Write Memory Log entry (AM)

/check-day (anytime)
    +-- "What are you doing right now?"
    +-- Redirect if off track

/end-day (PM)
    +-- "How'd it go?"
    +-- Update tasks and projects
    +-- Clean up past meetings
    +-- Surface patterns (3x+ = flag)
    +-- Write Memory Log entry (PM)
```

### The Memory Log

The `LOG` section in `NOW.md` is the core learning mechanism. Each `/start-day` and `/end-day` adds a timestamped entry. Over time, this creates a pattern library that the coaching personality references:

- **3x rule:** If the same behavior appears 3+ times, the coach flags it
- **AM/PM markers:** Enable detection of missed sessions
- **Quotes:** Important user phrases are preserved verbatim for later reference

## MCP Dependencies (Optional)

Several commands can integrate with MCP servers for live data. These are optional -- commands degrade gracefully without them.

| Server | Used by | Purpose |
|--------|---------|---------|
| `google-calendar` | `start-day`, `list-meetings`, `prep-meeting` | Read calendar events |
| `atlassian` | (add your own commands) | Create/update Jira tickets |

To configure MCP servers, edit `~/.claude/mcp.json` (not part of this plugin).

## Extending the System

### Adding a new command

1. Create `commands/<name>.md`
2. Add YAML frontmatter with at minimum `description:`
3. Optionally restrict tools with `allowed-tools:`
4. Optionally add `argument-hint:` for commands that accept arguments
5. Use `/<name>` in Claude Code

### Adding more state files

1. Create the `.md` file at `~/.claude/`
2. Add to the ASSISTANT FILES table in `CLAUDE.md`
3. Reference from relevant commands

### Custom integrations

The Jira and calendar integrations in the original system are implemented as:
- Additional commands with tool-specific `allowed-tools`
- MCP server references in command files (e.g., `mcp__claude_ai_Atlassian__createJiraIssue`)
- Config sections in CLAUDE.md (cloud IDs, project keys, etc.)

Follow the same pattern for any external tool integration.

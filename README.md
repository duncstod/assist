# Assist

A personal assistant that runs in your terminal. Built as a [Claude Code plugin](https://docs.anthropic.com/en/docs/claude-code) with persistent markdown files.

It knows your stakeholders, preps your meetings, tracks your projects, and challenges you when you're avoiding the hard work.

## How It Works

The system is **16 slash commands** backed by **5 shared context files**. Every command reads the same stakeholder profiles, project state, and priorities -- so when you prep a meeting, it already knows who you're meeting, what projects involve them, and what you're trying to achieve.

State lives in markdown files at `~/.claude/`. Not a database, not a SaaS product -- just text files.

```
/assist::start-day    -> Morning kickoff: calendar, tasks, priorities, coaching
/assist::check-day    -> Midday: "What are you doing right now?"
/assist::end-day      -> Evening: capture wins, patterns, lessons
/assist::prep-meeting -> Stakeholder-aware meeting prep with talking points
```

A `COACH.md` file defines the assistant's personality. Mine is set to "direct, no coddling, ship over perfect."

## Install

### 1. Add the marketplace and install the plugin

```
/plugin marketplace add duncstod/assist
/plugin install assist@assist
```

### 2. Run first-time setup

```
/assist::setup-life
```

A 5-minute conversation builds your personalized system: identity, stakeholders, coaching personality, working modes, and missions. Five context files are created at `~/.claude/` and you're ready to go.

## Commands

### Daily Workflow
| Command | What it does |
|---------|-------------|
| `/assist::start-day` | Morning kickoff. Checks calendar, surfaces tasks, sets 3 priorities and MIT. |
| `/assist::check-day` | Quick midday check-in. Keeps you accountable. |
| `/assist::end-day` | Evening review. Captures wins, lessons, and patterns. |

### Meetings
| Command | What it does |
|---------|-------------|
| `/assist::prep-meeting` | Builds talking points, anticipated questions, and stakeholder context. |
| `/assist::review-meeting` | Post-meeting reflection. Captures follow-ups as tasks. |
| `/assist::list-meetings` | Shows upcoming meetings with prep status. |

### Projects
| Command | What it does |
|---------|-------------|
| `/assist::add-project` | Create a project with goals, stakeholders, and mission connection. |
| `/assist::project-status` | Quick update. Surface blockers, log progress. |
| `/assist::project-think` | Think through a decision or strategic question on a project. |
| `/assist::list-projects` | Overview of all active projects with status. |
| `/assist::close-project` | Archive a project. Capture lessons learned. |

### Tasks
| Command | What it does |
|---------|-------------|
| `/assist::add-task` | Add a task to your list. |
| `/assist::complete-task` | Mark tasks as done. |
| `/assist::list-tasks` | View tasks grouped by project, with filtering. |

### Setup
| Command | What it does |
|---------|-------------|
| `/assist::setup-life` | First-time setup. Creates all context files through conversation. |
| `/assist::add-stakeholder` | Add a stakeholder profile for meeting prep context. |

## State Files

Created by `/assist::setup-life` at `~/.claude/`:

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Your identity, stakeholders, preferences. Loaded every session. |
| `COACH.md` | Coaching personality: your mission, patterns, challenge style. |
| `NOW.md` | Today's priorities, task list, working mode, memory log. |
| `MEETING.md` | Meeting prep, upcoming meetings, meeting history. |
| `PROJECTS.md` | Active project index with status and stakeholders. |

Template versions of these files are in `templates/` for reference.

## Optional: MCP Integrations

Connect to external tools via [MCP servers](https://modelcontextprotocol.io/):

- **Google Calendar** -- Live calendar data in `/assist::start-day`, `/assist::list-meetings`, `/assist::prep-meeting`
- **Jira/Atlassian** -- Add your own ticket management commands
- **Any MCP server** -- The system is extensible

Configure in `~/.claude/mcp.json` (not part of this plugin).

## Architecture

See [ARCHITECTURE.md](ARCHITECTURE.md) for how shared context, the memory log, and the daily loop work together.

## License

MIT

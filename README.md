
```
 ██████╗ ██╗████████╗████████╗ ██████╗
 ██╔══██╗██║╚══██╔══╝╚══██╔══╝██╔═══██╗
 ██║  ██║██║   ██║      ██║   ██║   ██║
 ██║  ██║██║   ██║      ██║   ██║   ██║
 ██████╔╝██║   ██║      ██║   ╚██████╔╝
 ╚═════╝ ╚═╝   ╚═╝      ╚═╝    ╚═════╝
```

> **A self-improving skill system for Claude Code.**
> Tell it what to get better at. It finds the skill and installs it.
> Dispatch a team of agents to work on your task in parallel.

---

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│   $ claude                                                   │
│                                                              │
│   > /learn better ui design                                  │
│                                                              │
│   Searching for skills...                                    │
│   ✓ Found 12 results across GitHub and the web               │
│   ✓ Evaluated 5 candidate skills                             │
│   ✓ Installed: ui-design-expert                              │
│                                                              │
│   Skill "ui-design-expert" is now active.                    │
│   Claude Code will automatically apply modern UI/UX          │
│   principles when building interfaces.                       │
│                                                              │
│   > make me a dashboard for my app                           │
│                                                              │
│   (Claude now uses the installed skill automatically)        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## Team Mode

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│   $ claude                                                   │
│                                                              │
│   > /team build a dashboard with auth and analytics          │
│                                                              │
│   Dispatching team...                                        │
│                                                              │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐       │
│   │Researcher│  │Architect│  │ Builder │  │Reviewer │       │
│   │  ⣾ ...  │  │  ⣾ ...  │  │  ⣾ ...  │  │ waiting │       │
│   └─────────┘  └─────────┘  └─────────┘  └─────────┘       │
│                                                              │
│   ✓ Researcher: found existing components & tech stack       │
│   ✓ Architect: designed page layout & data flow              │
│   ✓ Builder: implemented dashboard with 4 widget panels      │
│   ✓ Reviewer: verified auth guards & accessibility           │
│                                                              │
│   All agents complete. Dashboard ready at src/dashboard.tsx  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

`/team` breaks your task into subtasks and spawns **2-5 specialized agents in parallel** — researcher, architect, builder, reviewer, designer — each working simultaneously. Like a dev team, not a solo engineer.

## How it works

```
  /learn [topic]
       │
       ▼
  ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
  │   Search     │────▶│  Evaluate   │────▶│  Synthesize │
  │  the web     │     │  results    │     │  best skill │
  └─────────────┘     └─────────────┘     └──────┬──────┘
                                                  │
                                                  ▼
                                          ┌─────────────┐
                                          │   Install    │
                                          │  to Claude   │
                                          └─────────────┘
```

1. **Search** — Queries GitHub, community repos, and the web for Claude Code skills and expert prompts
2. **Evaluate** — Filters for relevance, quality, safety, and specificity
3. **Synthesize** — Combines the best techniques into a single, focused skill file
4. **Install** — Drops it into `~/.claude/skills/` where Claude Code auto-discovers it

## Commands

```
┌────────────────────────────────────────────────────────────────┐
│ COMMAND                        │ DESCRIPTION                   │
├────────────────────────────────┼───────────────────────────────┤
│ /learn [topic]                 │ Find & install a new skill    │
│ /team [task]                   │ Parallel multi-agent dispatch │
│ /skills list                   │ Show all installed skills     │
│ /skills info [name]            │ Inspect a specific skill      │
│ /skills remove [name]          │ Uninstall a skill             │
└────────────────────────────────┴───────────────────────────────┘
```

## Examples

```bash
# Get better at building UIs
> /learn ui design

# Get better at writing tests
> /learn testing best practices

# Get better at security reviews
> /learn security auditing

# Get better at database design
> /learn sql and database optimization

# Dispatch a team to build a landing page
> /team build a landing page for my SaaS product

# Have multiple agents review your code
> /team review this PR for bugs, security, and performance

# See what you've learned
> /skills list

# Remove a skill
> /skills remove old-skill
```

## Installation

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/elvinmonke/ditto.git ~/.claude/skills

# That's it. The skills are available immediately.
```

If you already have a `~/.claude/skills/` directory, clone into a temp location and copy the skill folders:

```bash
git clone https://github.com/elvinmonke/ditto.git /tmp/ditto
cp -r /tmp/ditto/learn ~/.claude/skills/
cp -r /tmp/ditto/skills ~/.claude/skills/
rm -rf /tmp/ditto
```

## How skills work

Skills are markdown files that live in `~/.claude/skills/<name>/SKILL.md`. Claude Code automatically discovers them — no restart needed.

```
~/.claude/skills/
├── learn/            ← finds & installs new skills
│   └── SKILL.md
├── team/             ← parallel multi-agent dispatcher
│   └── SKILL.md
├── skills/           ← manages installed skills
│   └── SKILL.md
└── ui-design/        ← example: installed by /learn
    └── SKILL.md
```

Skills can be:
- **Auto-invoked** — Claude uses them automatically when relevant
- **Manual** — You trigger them with `/skill-name`
- **Background** — Always-on context Claude draws from silently

## License

MIT

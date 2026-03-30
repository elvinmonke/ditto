
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

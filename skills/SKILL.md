---
name: skills
description: List, inspect, or remove installed Claude Code skills
disable-model-invocation: true
argument-hint: [list | info <name> | remove <name>]
allowed-tools: Read, Bash(ls *), Bash(rm *), Glob, Grep
---

# Skill Manager

Manage installed Claude Code skills based on the command: **$ARGUMENTS**

## Commands

### `list` (or no arguments)
List all installed skills from both locations:
- User-level: `~/.claude/skills/`
- Project-level: `.claude/skills/`

For each skill, show:
- Name
- Description (from frontmatter)
- Scope (user/project)
- Auto-invoked or manual

Format as a clean table.

### `info <name>`
Show full details of a specific skill:
- Read and display the SKILL.md frontmatter
- Show the skill's instructions (summarized if long)
- List any supporting files in the skill directory

### `remove <name>`
Remove an installed skill:
1. Confirm with the user before deleting
2. Delete the skill directory from `~/.claude/skills/<name>/`
3. Confirm removal

## How to Find Skills

Read the `SKILL.md` file in each subdirectory of `~/.claude/skills/` and `.claude/skills/`.
Parse the YAML frontmatter between `---` markers to extract metadata.

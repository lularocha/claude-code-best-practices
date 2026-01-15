# Claude Skills

## What They Are

**Skills** are folders containing instructions, scripts, and resources (with a `SKILL.md` file) that Claude automatically loads when relevant to your task.

## Key Points

- Transform Claude from general-purpose to specialized for specific tasks
- Pre-built skills exist for documents (PowerPoint, Excel, Word, PDF)
- Custom skills: create a folder with `SKILL.md` and Claude discovers them automatically
- Progressive disclosure: loads only what's needed, keeping context efficient
- Released as an **open standard** (December 2025) - adopted by OpenAI too

## How Skills Work

At its simplest, a skill is a directory that contains a `SKILL.md` file. This file must start with YAML frontmatter containing required metadata: `name` and `description`.

At startup, Claude pre-loads the name and description of every installed skill. The description field is how Claude decides whether to use your Skill.

### Good Description Example

A good description answers two questions:
1. **What does this Skill do?** - List the specific capabilities
2. **When should Claude use it?** - Include trigger terms users would mention

### Best Practices

- Keep `SKILL.md` under 500 lines for optimal performance
- If content exceeds this, split detailed reference material into separate files
- Claude discovers supporting files through links in your `SKILL.md`

## Installation

Skills can be installed in Claude Code by:
- Installing plugins from the [anthropics/skills marketplace](https://github.com/anthropics/skills)
- Manually adding skills to `~/.claude/skills`
- Sharing skills through version control with your team

---

## References

- [Agent Skills - Claude Code Docs](https://code.claude.com/docs/en/skills)
- [GitHub - anthropics/skills](https://github.com/anthropics/skills)
- [Introducing Agent Skills | Anthropic](https://www.anthropic.com/news/skills)

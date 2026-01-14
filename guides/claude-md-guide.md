# CLAUDE.md

CLAUDE.md is a markdown file that Claude automatically reads at the start of each session. It holds project-specific instructions you'd otherwise repeat in every prompt. Structure, conventions, workflows, style.

### CLAUDE.md files should not be static. Review and improve them regularly.

## How to create a CLAUDE.md file

- **From scratch:** Create a markdown file and start writing. 

- **Get Claude to create it for you:** Run the `/init` command in your project directory. Claude will create a starter CLAUDE.md based on your project structure and tech stack. You can then review, edit, and refine it to your needs.

- ⚠️ **The filename is case-sensitive** — it must be exactly `CLAUDE.md` (CLAUDE in uppercase, .md in lowercase).

## Setup

I'm using a two-level structure for my CLAUDE.md files:

1. **Top-level CLAUDE.md** – Located at the root of my workspace, this file contains general instructions for how Claude should write code across all projects.

2. **Project-specific CLAUDE.md** – Each project folder has its own CLAUDE.md with context and conventions specific to that codebase.

Claude reads both files, with project-specific instructions taking precedence when relevant.

## Top-level CLAUDE.md 

These are the instructions I'm experimenting with:

1. Think through problems, read the codebase first
2. Check in before major changes
3. Ask clarifying questions
4. Give high-level explanations of changes
5. Keep changes simple and minimal
6. Maintain architecture documentation
7. Never speculate about unread code
8. Read relevant files before answering codebase questions
9. Give grounded, hallucination-free answers
10. Run tests after making changes to verify nothing broke

## Project-specific CLAUDE.md 

A well-structured CLAUDE.md gives Claude the context it needs to write code that fits your project. Here are the key sections to include:

- **Project Title and Description** – Start with the project name and a one-line description. This gives Claude immediate context about what the codebase does.

- **Code Style** – Define your coding conventions: language settings, export patterns, formatting preferences, CSS approach, etc. Be specific about what to use and what to avoid.

- **Commands** – List the essential commands for development, testing, linting, and deployment. Claude can then run the right commands without asking.

- **Architecture** – Map out your folder structure and explain what each directory contains. This helps Claude understand where to find and place code.

- **Important Notes** – Highlight critical rules, security considerations, and gotchas. This is where you put things Claude should never forget—like files that shouldn't be committed or APIs that require special handling.

### Example

```markdown
# Project: Your Project Title

A one-line description of what this project does.

## Code Style

- Use ES6+ syntax (arrow functions, destructuring, template literals)
- Prefer `const` over `let`, avoid `var`
- Use meaningful variable and function names
- Keep functions small and single-purpose

## Commands

- `npm run dev`: Start development server
- `npm run build`: Build for production
- `npm run test`: Run tests
- `npm run lint`: Check for code issues

## Architecture

- `/src`: Main source code
- `/src/components`: Reusable UI components
- `/src/utils`: Helper functions and utilities
- `/src/api`: API calls and data fetching
- `/public`: Static assets (images, fonts)

## Important Notes

- NEVER commit `.env` files—they contain sensitive API keys
- All external API calls go through `/src/api` to centralize error handling
- Run `npm run lint` before committing
```

## Best Practices

- **Add Instructions** – Add instructions as you work, for example, if you notice Claude doing something wrong, don't just fix it, add or edit instructions to prevent the same mistake. 

- **Ask Claude for Help** – You can ask Claude to review and suggest improvements to your CLAUDE.md files.

- **Review and improve regularly** 

## References

Many developers share their CLAUDE.md setups and results online. I get good insights from the people I follow on Twitter/X.

To create this page, I drew from [The Complete Guide to CLAUDE.md by Vishwas](https://x.com/codevolutionweb/status/2010715163859542086) (which covers more advanced setups), Alex Finn's [tutorial on Claude Code Desktop](https://www.youtube.com/watch?v=pZ2N7CJFbBk), and Claude itself—asking it for suggestions and clarifications.
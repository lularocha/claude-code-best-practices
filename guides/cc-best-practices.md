# Best Practices

## Fundamentals

### Talk to Claude Like a Colleague

Think of Claude Code as a conversation with an intelligent colleague, not just a tool. Before accepting any answer, ask for clarification or have Claude ask you questions to ensure you both have a clear understanding of the task and the plan to accomplish it. Just like discussing a project with a coworker, back-and-forth dialogue leads to better outcomes.

### Use CLAUDE.md

CLAUDE.md is a markdown file that Claude automatically reads at the start of each session. Place it in the root of your project folder or a parent directory for shared instructions across projects. It holds context and instructions you'd otherwise repeat in every prompt.

For more information on creating and structuring CLAUDE.md files, see the [CLAUDE.md Guide](claude-md-guide.md).

### Be Specific

Clear, detailed instructions get better results. Instead of vague requests like "make it better," describe exactly what you want: the behavior, the constraints, the expected output. The more context you provide upfront, the less back-and-forth you'll need.

### Use Visuals

Paste screenshots directly into your conversation for UI and design work. Claude can analyze images to understand layouts, identify issues, or implement designs. This is especially useful when describing visual bugs or mocking up new features.

### Use Plan Mode

Start complex tasks with `/plan` to think through the approach before writing code. Ask Claude to ask you questions to refine the plan. Useful prompts include:

- "Ask me questions to understand what I'm looking for"
- "What else do you need to know to have a clear picture?"

### Connect to GitHub

Connect your project folder as a Git repository. This enables Claude to create branches, commit changes, open pull requests, and review code through natural conversation. Version control provides a safety net—you can easily revert changes if something goes wrong and track the evolution of your project over time.

### Verify Your Work

After completing a section or significant work, ask Claude to verify everything. Review the changes yourself before moving on. A useful prompt:

- "Go back and verify all the work done. Make sure you used best practices for efficiency, maintainability, and security."

Consider creating a slash command for this verification task to run it regularly.

### Use /clear

Use the `/clear` command to reset context between unrelated tasks. This prevents confusion from previous conversations bleeding into new ones and keeps Claude focused on the current task.

### Start Small and Iterate

Build incrementally rather than trying to implement everything at once. Start with a minimal working version, verify it works, then add features one at a time. This approach makes debugging easier and ensures each piece works before adding complexity.

---

## Advanced

### Create Slash Commands

Slash commands automate repetitive tasks and save significant time. Ask Claude to help you create them:

- "What are some useful slash commands that can save me time?"
- "Make me a slash command that commits and pushes all code to GitHub"

Commands can be global or project-specific depending on your needs.

### Use Git Workflows

Beyond basic commits, leverage full Git workflows: feature branches for isolation, pull requests for code review, and meaningful commit messages for history. Claude can help manage these workflows conversationally, making version control more accessible.

### Use MCP Servers

Model Context Protocol (MCP) servers connect Claude to external tools and data sources. This extends Claude's capabilities to interact with databases, APIs, file systems, and other services beyond the local codebase.

### Use Skills

Skills are specialized instruction sets that extend Claude's capabilities for specific tasks. They provide domain expertise and workflows that go beyond general coding assistance, such as PR reviews, documentation generation, or framework-specific patterns.

### Multi-Claude Workflows

Run parallel Claude instances for complex work. Use one instance for planning, another for implementation, or split work across different parts of a codebase. This approach helps maintain focus and can speed up larger projects.

### Use Headless Mode

Run Claude in CI pipelines or scripts using the `-p` flag for non-interactive execution. This enables automated code generation, testing, and other tasks without manual intervention—useful for scheduled tasks or integration into existing workflows.

### Customize with Hooks

Extend Claude's behavior with custom scripts that run at specific points in the workflow. Hooks let you add validation, formatting, notifications, or any custom logic that integrates Claude into your development process.

---

## References

- [Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices) - Anthropic Engineering

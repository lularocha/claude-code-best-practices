# Best Practices Overview

## AGI Mindset

**AGI (Artificial General Intelligence)** refers to AI systems that can understand, learn, and perform any intellectual task that a human can do, across different domains without being specifically trained for each one.

Think of Claude Code as a conversation with an AGI person, not just a tool. Before accepting any answer, ask for clarification or have the model ask you questions to ensure both you and Claude have a clear understanding of the task and the plan to accomplish it. Just like discussing a project with a work collegue.

## Use CLAUDE.md

**Location:** Root of your project folder or parent directory for all projects.

CLAUDE.md is a markdown file that Claude automatically reads at the start of each session. It holds instructions you'd otherwise repeat in every prompt.

For a complete guide on creating and structuring CLAUDE.md files, see the [CLAUDE.md Guide](claude-md-guide.md).

## Connect to GitHub

Connect your project folder as a repository in your GitHub account. This enables Claude Code to leverage powerful Git integrations—creating branches, committing changes, opening pull requests, and reviewing code—all through natural conversation. Version control also provides a safety net, allowing you to easily revert changes if something goes wrong and track the evolution of your project over time.

## Work in Plan Mode

Always refine the plan as much as needed by asking Claude to ask you questions.

**Useful prompts:**

- "Ask me questions for you to find out more about what I'm looking for"  
- "Any other things I can answer to give you a clear picture of what I'm looking for?"

## Work with Slash Commands

Slash commands can save significant time by automating repetitive tasks.

**How to get started:**

- Prompt: "What are some useful slash commands that can save me time?" (either globally or for a specific project)

**Example:**

- "Make me a slash command that commits and pushes all our code to github"

## Diligence - Verify the Work Done

After completing a section or significant work, ask Claude to verify everything.

**Prompt:**

- "Go back and verify all the work done so far. Make sure you used the best coding practices for efficiency, maintainability, and security."

**Tip:** Create a slash command for this verification/diligence task to make it easier to run regularly.

## Create a CEO for Every Project

**What is a CEO?** A CEO (Chief Executive Officer) is a specialized prompt/agent that understands your entire project and can manage it end-to-end.

**When to create:** After everything is done and works well, create the CEO using the initial project prompt.

**Source:** [Alex's video on working with Claude Code Desktop](https://www.youtube.com/watch?v=pZ2N7CJFbBk)

## Important Things to Remember

A running log of miscellaneous but important practices:

- **Rename Conversations** \- Give your conversations descriptive names to easily find and reference them later  
- **Finding Past Conversations** \- Use `/history` command to view all past conversations and resume from where you left off


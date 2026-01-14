# CLAUDE.md

CLAUDE.md is a markdown file that Claude automatically reads at the start of each session. It holds project-specific instructions you'd otherwise repeat in every prompt. Structure, conventions, workflows, style.

## Setup

I use a two-level structure for my CLAUDE.md files:

1. **Top-level CLAUDE.md** – Located at the root of my workspace, this file contains general instructions for how Claude should write code across all projects.

2. **Project-specific CLAUDE.md** – Each project folder has its own CLAUDE.md with context and conventions specific to that codebase.

Claude reads both files, with project-specific instructions taking precedence when relevant.

## How to structure a project CLAUDE.md file

A well-structured CLAUDE.md gives Claude the context it needs to write code that fits your project. Here are the key sections to include:

### Project Title and Description

Start with the project name and a one-line description. This gives Claude immediate context about what the codebase does.

### Code Style

Define your coding conventions: language settings, export patterns, formatting preferences, CSS approach, etc. Be specific about what to use and what to avoid.

### Commands

List the essential commands for development, testing, linting, and deployment. Claude can then run the right commands without asking.

### Architecture

Map out your folder structure and explain what each directory contains. This helps Claude understand where to find and place code.

### Important Notes

Highlight critical rules, security considerations, and gotchas. This is where you put things Claude should never forget—like files that shouldn't be committed or APIs that require special handling.

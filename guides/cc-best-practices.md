# Claude Code Best Practices

## AGI Mindset

**AGI (Artificial General Intelligence)** refers to AI systems that can understand, learn, and perform any intellectual task that a human can do, across different domains without being specifically trained for each one.

Think of Claude Code as a conversation with an AGI person, not just a tool. Before accepting any answer, ask for clarification or have the model ask you questions to ensure both you and Claude have a clear understanding of the task and the plan to accomplish it.

## CLAUDE.md (Claude Instructions)

**Location:** Root of your project folder or parent directory for all projects.

[Learn more about CLAUDE.md](claude-md-guide.md)

### **Instructions:**

1. First think through the problem, read the codebase for relevant files.  
2. Before you make any major changes, check in with me and I will verify the plan.  
3. Ask me questions for you to better understand what I want to accomplish and how.  
4. Please every step of the way just give me a high level explanation of what changes you made.  
5. Make every task and code change you do as simple as possible. We want to avoid making any massive or complex changes. Every change should impact as little code as possible. Everything is about simplicity.  
6. Maintain a documentation file that describes how the architecture of the app works inside and out.  
7. Never speculate about code you have not opened. If the user references a specific file, you MUST read the file before answering.  
8. Make sure to investigate and read relevant files BEFORE answering questions about the codebase.  
9. Never make any claims about code before investigating unless you are certain of the correct answer \- give grounded and hallucination-free answers.

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

## Verify the Work Done (Diligence)

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


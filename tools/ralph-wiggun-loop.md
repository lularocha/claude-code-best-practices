# Ralph Wiggun Loop

## IMPORTANT NOTE

**Don't use Anthropic's plugin version, use the original Geoffrey Huntley vision**

More info: https://x.com/gmickel/status/2009939771171434867
Geoffrey Huntley on Twitter: https://x.com/GeoffreyHuntley

---

## What It Is

**Ralph Wiggun Loop** is a technique for running Claude Code autonomously in a loop until a task is complete.

> "Ralph is a Bash Loop" — Geoffrey Huntley

### The Core Concept

Instead of giving Claude one shot at a task and hoping it gets it right, you run it repeatedly on the same task. Each time it runs, Claude sees its previous work (via git history and modified files), learns from what broke, and tries again until it succeeds.

### Why It Works

- **Fresh context per iteration**: Each loop starts with a clean slate. Claude doesn't accumulate unnecessary conversation history or context pollution from previous attempts. The git history and file changes provide all the context needed.
- **Iterative learning**: Claude can see what failed and fix it by examining git history and error messages
- **Feedback loops**: Tests, linting, and type checking provide clear pass/fail signals
- **Autonomous execution**: No manual intervention needed between iterations

#### Advantages

- **No context pollution**: Unlike a long single session where the conversation history keeps growing with failed attempts, explanations, and dead-end explorations
- **Efficient context usage**: Only the relevant information (current code state + git history + the task prompt) is in context
- **No token waste**: You don't pay for accumulated conversation context from previous failed attempts
- **Clear signal-to-noise ratio**: Claude only sees what matters - the current code state and the task

### Key Principles

1. **Clear completion criteria** — Claude needs to know when it's truly done (e.g., "all tests pass")
2. **Scoped tasks** — Break work into specific, completable pieces
3. **Safety limits** — Always set a maximum iteration count
4. **Git tracking** — Run in a git repository so you can revert if needed

---

## How to Use It

### Basic Bash Loop

The simplest implementation is a bash script that repeatedly calls `claude-code` until completion:

```bash
#!/bin/bash

MAX_ITERATIONS=10
PROMPT="Your task description here. When complete, output DONE on a single line."

for i in $(seq 1 $MAX_ITERATIONS); do
  echo "Iteration $i of $MAX_ITERATIONS"

  OUTPUT=$(echo "$PROMPT" | claude-code)
  echo "$OUTPUT"

  # Check if Claude signals completion
  if echo "$OUTPUT" | grep -q "DONE"; then
    echo "Task completed successfully!"
    exit 0
  fi

  # Brief pause between iterations
  sleep 2
done

echo "Max iterations reached. Task may be incomplete."
exit 1
```

### Writing Effective Prompts

Your prompt should include:

1. **The task** — What needs to be done
2. **Completion criteria** — How Claude knows it's finished
3. **Feedback instructions** — What to check after each change (tests, builds, etc.)
4. **Git instructions** — When to commit

**Example prompt:**

```
Add unit tests for all functions in src/utils/parser.js.

Instructions:
- Write one test file at a time
- Run tests after each file: npm test
- Fix any failures before moving to the next file
- Commit after each passing test file
- When ALL functions have tests and ALL tests pass, output: DONE

Completion criteria:
- Test coverage for all functions
- All tests passing
- No errors or warnings
```

### Using PROMPT.md Files

Instead of inline prompts, put instructions in a file:

**PROMPT.md:**
```markdown
# Task
Add form validation to the contact form

## Requirements
- Validate email format
- Require all fields
- Show error messages

## Process
1. Write validation logic
2. Add error message display
3. Write tests for validation
4. Run: npm test
5. Fix any failures
6. When tests pass, commit and output: DONE
```

**Bash script:**
```bash
#!/bin/bash
MAX_ITERATIONS=15
PROMPT=$(cat PROMPT.md)

for i in $(seq 1 $MAX_ITERATIONS); do
  echo "Iteration $i"
  OUTPUT=$(echo "$PROMPT" | claude-code)
  echo "$OUTPUT"

  if echo "$OUTPUT" | grep -q "DONE"; then
    echo "Complete!"
    exit 0
  fi
  sleep 2
done
```

### Using PRD (Product Requirements Document) Files for Multi-Task Projects

For larger projects, use a JSON file to track multiple tasks:

**PRD.json:**
```json
{
  "project": "Contact Form Feature",
  "tasks": [
    {
      "id": 1,
      "description": "Create ContactForm component",
      "completed": false
    },
    {
      "id": 2,
      "description": "Add field validation",
      "completed": false
    },
    {
      "id": 3,
      "description": "Add error message display",
      "completed": false
    }
  ]
}
```

**PROMPT.md:**
```markdown
# Instructions

1. Read PRD.json
2. Find the first task where "completed": false
3. Work on ONLY that task
4. Run tests when done
5. If tests pass:
   - Update the task's "completed" to true in PRD.json
   - Commit with message: "Complete task #[id]: [description]"
6. When ALL tasks are completed, output: DONE
```

### Best Practices

1. **Start small** — Test with 3-5 iterations first
2. **Use git** — Always work in a git repository
3. **Set limits** — Don't let loops run indefinitely
4. **Verify completion** — Make sure Claude has a clear way to signal "done"
5. **Use tests** — Automated tests give Claude the best feedback
6. **Review output** — Check what happened after the loop finishes

### Example: Complete Working Script

```bash
#!/bin/bash

MAX_ITERATIONS=20
TASK="Fix all TypeScript errors in src/ directory. Run 'npm run type-check' after each fix. When there are zero errors, output: DONE"

echo "Starting Ralph Loop..."
echo "Task: $TASK"
echo "Max iterations: $MAX_ITERATIONS"
echo "---"

for i in $(seq 1 $MAX_ITERATIONS); do
  echo ""
  echo "=== Iteration $i of $MAX_ITERATIONS ==="

  OUTPUT=$(echo "$TASK" | claude-code 2>&1)

  echo "$OUTPUT"

  # Check for completion signal
  if echo "$OUTPUT" | grep -q "DONE"; then
    echo ""
    echo "✓ Task completed successfully on iteration $i"
    git log -1 --oneline
    exit 0
  fi

  # Pause between iterations
  sleep 3
done

echo ""
echo "✗ Max iterations reached. Check git log for progress."
exit 1
```

---

## References

**Geoffrey Huntley** — [https://x.com/GeoffreyHuntley](https://x.com/GeoffreyHuntley)

[Ralph Wiggum: Claude Code's new way to run autonomously](https://medium.com/@joe.njenga/ralph-wiggum-claude-code-new-way-to-run-autonomously-for-hours-without-drama-095f47fbd467)
by [Joe Njenga](https://medium.com/@joe.njenga)  

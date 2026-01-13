# Ralph Wiggun \- Loop Plugin

## IMPORTANT NOTE

**Don't use Anthropic's version, use the original Geoffrey Huntley vision**

More info: https://x.com/gmickel/status/2009939771171434867
Geoffrey Huntley on Twitter: https://x.com/GeoffreyHuntley

---

**Ralph Wiggum** is a technique/plugin for Claude Code that makes the AI work autonomously in a loop until a task is complete. "Ralph is a Bash Loop \- Geoffrey Huntley"

**The core idea:** instead of giving Claude one shot at a task and hoping it gets it right, you run it repeatedly on the same task. Each time it runs, it sees its previous work (via git history and modified files), learns from what broke, and tries again until it succeeds.

The technique was originally created by Geoffrey Huntley as a simple bash loop, and Anthropic later formalized it into an official Claude Code plugin.

**One-liner:** A plugin that runs Claude Code in a loop, iterating on a task until verifiable completion criteria are met — enabling autonomous, unsupervised coding.

**In other words: it makes Claude Code keep trying until the job is done.**

**Use it with PROMPT.md or PRD (Product Requirements Document) Files**

* **PROMPT.md** \= Good for single-scope tasks  
* **PRD.json** 	\= Good for multi-task projects

**Best use: Integrate both PROMPT.md and PRD File**

* **PROMPT.md** \= the rules (how to work)  
* **PRD.json** \= the work (what to do)

## Creating and using the PROMPT

1. **Define a clear, scoped task**

   Don't give it vague or massive tasks. Break work into specific, completable pieces. Good: "Add unit tests to all functions in src/utils/". Bad: "Build me an app".

2. **Set strong completion criteria**

   Give Claude a way to verify it's actually done — ideally something testable like "all tests pass" and "no TypeScript errors". The completion promise should only be output when that criteria is met.

3. **Use feedback loops**

   The technique works best when Claude can verify its own work. TypeScript type checking, unit tests, linting — anything that gives Claude clear pass/fail signals to learn from.

4. **Always set a max-iterations limit**

   This is your safety net to prevent runaway loops and cost overruns.

5. **Run in a git-tracked directory**

   So you can revert if something goes wrong, and so Claude can see the history of what it changed.

**/ralph-loop**   
"\[TASK\] \+ \[FEEDBACK INSTRUCTION\] \+ \[GIT INSTRUCTION\] \+ \[COMPLETION CRITERIA\]" \--max-iterations X \--completion-promise "YOUR\_PROMISE"

**Example (Command/Prompt:**

/ralph-loop "Build a contact form component with fields for name, email, and message. Include validation (required fields, valid email format). Write unit tests for the validation logic. Run tests and type check after each change. Commit after all tests pass and there are no type errors. If all tests pass, type check passes, and the component renders without errors, output \<promise\>COMPLETE\</promise\>." \--max-iterations 15 \--completion-promise "COMPLETE"

**What happens:**

1. Claude creates the component and tests  
2. Claude runs the tests  
3. Tests fail (maybe validation logic is wrong)  
4. Claude tries to exit → Stop hook blocks it  
5. Claude sees the test failures, fixes the code  
6. Runs tests again  
7. Tests pass → Claude commits the changes  
8. Repeats until all work is complete  
9. Claude outputs `<promise>COMPLETE</promise>`  
10. Loop ends

## PROMPT.md

Instead of writing a long prompt inline in the command, you **put instructions in a file and reference it**.

Example:

\# Task  
Build a contact form component for a portfolio website.

\#\# Requirements  
\- Fields: name, email, message  
\- Validation: all fields required, email must be valid format  
\- Display error messages below each invalid field

\#\# Instructions  
\- Work on one requirement at a time  
\- Write unit tests for validation logic  
\- Run tests after each change  
\- Commit after each passing test run  
\- If all tests pass and the component renders without errors, output \<promise\>COMPLETE\</promise\>

**How to use it**  
/ralph-loop \--prompt PROMPT.md \--max-iterations 15 \--completion-promise "COMPLETE"

## PRD File (JSON)

A structured list of tasks to complete  
Dynamic — Claude updates it as tasks are completed

**Example/JSON**  
{  
  "project": "Portfolio Contact Form",  
  "tasks": \[  
    {  
      "id": 1,  
      "description": "Create basic ContactForm component with name, email, message fields",  
      "passes": false  
    },  
       {  
      "id": 3,  
      "description": "Display error messages below invalid fields",  
      "passes": false  
    },  
    {  
      "id": 3,  
      "description": "Write unit tests for all validation logic",  
      "passes": false  
    }  
  \]  
}

**How Claude uses it:**

1. Claude reads the PRD  
2. Picks the first task with `"passes": false`  
3. Completes that one task only  
4. Runs tests  
5. If tests pass → updates `"passes": true` and commits  
6. Loop continues → Claude picks the next incomplete task  
7. Repeats until all tasks have `"passes": true`

---

**Why use this?**

* Prevents Claude from trying to do everything at once (avoids context window overload)  
* Tracks progress across multiple loop iterations  
* You can see exactly what's done and what's left

## PROMPT.md \+ PRD File

**PROMPT.md** (the instructions):

\# Contact Form Development

\#\# How to work  
1\. Read PRD.json to find the next task with "passes": false  
2\. Work on ONLY that single task  
3\. Write or update tests for the task  
4\. Run tests after each change  
5\. If tests pass:  
   \- Update the task's "passes" to true in PRD.json  
   \- Commit with message: "Complete task \#\[id\]: \[description\]"  
6\. If all tasks in PRD.json have "passes": true, output \<promise\>COMPLETE\</promise\>

**PRD.json** (the task list):

{  
  "project": "Portfolio Contact Form",  
  "tasks": \[  
    {  
      "id": 1,  
      "description": "Create basic ContactForm component with name, email, message fields",  
      "passes": false  
    },  
    {  
      "id": 2,  
      "description": "Add validation logic for required fields",  
      "passes": false  
    },  
    {  
      "id": 3,  
      "description": "Add email format validation",  
      "passes": false  
    }  
  \]  
}

**The Command**

/ralph-loop \--prompt PROMPT.md \--max-iterations 20 \--completion-promise "COMPLETE"

**What happens:**

1. Claude reads PROMPT.md → learns how to work  
2. Claude reads PRD.json → finds task \#1 (`"passes": false`)  
3. Completes task \#1, runs tests  
4. Tests pass → updates PRD.json (`"passes": true`), commits  
5. Loop continues → Claude finds task \#2  
6. Repeats for each task  
7. All tasks complete → outputs `<promise>COMPLETE</promise>`  
8. Loop ends

---

### The key insight

* **PROMPT.md** \= the rules (how to work)  
* **PRD.json** \= the work (what to do)

They're separate so you can reuse the same PROMPT.md across different projects, just swap the PRD.

---

## References

Matt Pocock
[https://www.aihero.dev/](https://www.aihero.dev/)
[https://x.com/mattpocockuk/status/2010045508765782433?s=20](https://x.com/mattpocockuk/status/2010045508765782433?s=20)

Joe Njenga on Medium  
[https://medium.com/@joe.njenga/ralph-wiggum-claude-code-new-way-to-run-autonomously-for-hours-without-drama-095f47fbd467](https://medium.com/@joe.njenga/ralph-wiggum-claude-code-new-way-to-run-autonomously-for-hours-without-drama-095f47fbd467)

Anthropic blog \- Effective Harnesses for long running agents  
[https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

Geoffrey Huntley  
[https://x.com/GeoffreyHuntley](https://x.com/GeoffreyHuntley)  

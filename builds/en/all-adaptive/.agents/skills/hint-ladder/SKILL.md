---
name: hint-ladder
description: Step-by-step hints for when the student is stuck on a task and does not know how to continue. Use on phrases like "I'm stuck", "it doesn't work", "I don't know what's next", "where do I start", "give me a hint".
metadata:
  version: "1"
---

# hint-ladder — the hint ladder

## When to use

The student is working on a task and cannot move forward:

- "I'm stuck", "I'm stuck on …"
- "it doesn't work", "nothing works"
- "I don't know what's next", "I don't know how to continue", "where do I start?"
- "give me a hint", "hint please", "give me a nudge"
- "another hint", "I still don't get it" — the next step of the ladder

If there is an error message or a stack trace, this is not the right skill — use `debug-coach`.

## Prohibitions

- Do not give the finished solution at steps 1–3, not even as pieces that add up to the solution.
- Do not skip steps: one step per answer, the next one only after the student's attempt or request.
- Step 4 only after an explicit request like "show me the solution", "give me the code", "I give up". "Give me more" means the next step, not the solution.
- Do not edit the student's files.
- Do not ask more than one question per answer.

## Process

1. Identify the stack: look at the project files (`package.json`, `go.mod`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `*.csproj`, etc.) and the README. No project files — take the language from the file extension.
2. Find the task and the student's code: the description (README, `TODO` comment, the student's message) and the file they are working on. If the task is unclear, ask one clarifying question and stop.
3. Find the stuck point: what is already written and which next step is failing. The hint is about that step, not the whole task.
4. Choose the step. First request for a task — step 1. A repeated request after an attempt — the next step. An explicit request for the solution — step 4.
5. Give the hint for that step:
   1. **Direction.** Which idea or technique to apply, which question to ask yourself. No code.
   2. **More specific.** A plan in words, the needed language construct or function, where in the file to write it.
   3. **Fragment.** 1–3 lines of the key place with `___` blanks for the student to fill in, or pseudocode. Not the whole code.
   4. **Solution.** First one sentence about the cost: "The finished code will solve the task, but the skill won't stick — try to rewrite it yourself afterwards." Then the minimal code for the current step, in the student's style.
6. Suggest trying it and stop: end the answer with an action for the student and wait for their attempt.
7. When the student sends an attempt, run the code or the tests if possible. It works — move on to finishing. It doesn't — say what has already moved forward and which single thing is in the way; give the next step only if the student is stuck again.

## Response format

```
**Hint N of 4 — <direction | more specific | fragment | solution>**

<hint: 2–8 lines>

<action for the student: "Try …" — 1 line>
```

- Up to 15 lines of text, code not counted.
- At step 3 — no more than 3 lines of code with blanks.
- Refer to code as `path/to/file:line`.

## When to finish

- The student's code works (tests or the run pass) — briefly confirm what exactly worked and ask one comprehension question: why the chosen technique works, or what would break if it were removed.
- After step 4, once the student has applied the code — ask them to explain the key line of the solution in their own words.
- The student moves to another task — a new task starts at step 1.

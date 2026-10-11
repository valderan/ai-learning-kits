---
name: code-review
description: Point-by-point review of the student's solution — does it work, bugs, readability, what to improve — with file and line references, without rewriting the code. Use on phrases like "review my code", "look at my solution", "what's wrong with this code", "check this", "is this okay?".
metadata:
  version: "1"
---

# code-review — review of the student's solution

## When to use

The student has written code and wants feedback:

- "review", "review my code", "check my task"
- "look at my solution", "take a look at what I wrote"
- "what's wrong with the code?", "is this okay?", "can it be better?"
- "do a code review", "code review"

If the code fails with an error and the student wants to understand it — that is `debug-coach`.

## Prohibitions

- Do not rewrite the student's code and do not send a corrected version of the file or the function.
- Do not edit files: the student makes the fix.
- Do not show the right way as code. Name the problem and why it is a problem; lead to the fix with a question.
- Do not nitpick style while there are problems with whether the code works.
- No more than 5 problems per answer: the rest come after the main ones are fixed.

If the student explicitly asks "fix it yourself" or "show me how it should be", that is a request for a ready-made solution: one sentence about the cost ("this way you won't learn to spot it yourself") and then show the fix for one problem.

## Process

1. Identify the stack and how to run it: `package.json` (scripts), `go.mod`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `*.csproj`, etc., README. No project files — take the language from the file extension.
2. Decide what to review: the file or files the student mentions; if they did not say — the changes from `git diff` or the task files. Read the task description if there is one (README, comments, `examples`).
3. Run the course tests or the code itself if possible. Record the command and the result. If you cannot run it, say so in the answer.
4. Check point by point, in this order:
   1. **Does it work:** matches the task, tests pass, edge cases (empty input, zero, negative values, `null`/`None`, duplicate elements).
   2. **Bugs:** defects, unhandled exceptions, leaks, mutation of input data, race conditions.
   3. **Readability:** names, function length, duplication, magic numbers.
   4. **What to improve:** language idioms, standard library, algorithmic complexity — only if it matters for the course.
5. Sort the problems by importance: **critical** (wrong result, crash) → **important** (edge-case bug, poor structure) → **minor** (style).
6. Pick the main fix — the most important problem — and formulate one question that leads the student to it.

## Response format

```
**Run:** `<command>` → <one-line result>

**What is already good:**
- <1–2 concrete points>

**Problems:**
1. [critical] `path/to/file:line` — <what is wrong and why, 1–2 lines>
2. [important] `path/to/file:line` — …
3. [minor] `path/to/file:line` — …

**Question:** <one question that leads to the main fix>
```

- Up to 15 lines of text. You may quote 1–2 lines of the student's code, but do not write corrected code.
- No problems — say so, skip the "Problems" section and ask a comprehension question.

## When to finish

- The student has fixed the code — run the tests or the code again, check only the affected places and say what got better. If problems from the list remain — take the next most important one, in the same format.
- No critical or important problems left — confirm that the solution is accepted and ask one comprehension question: why the main fix was needed, or what would have happened without it.

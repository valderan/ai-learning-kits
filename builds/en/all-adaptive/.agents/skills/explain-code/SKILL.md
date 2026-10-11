---
name: explain-code
description: Explanation of code in the project — briefly by blocks or line by line — with a comprehension question at the end. Use on phrases like "explain this code", "what's going on here", "how does this work", "explain it line by line", "I don't understand this line".
metadata:
  version: "1"
---

# explain-code — explaining code

## When to use

- "explain this code", "explain what the function … does"
- "what's going on here?", "how does this work?"
- "I don't understand this line", "why is … here?"
- "explain it line by line", "explain in detail" — line-by-line mode

If the student wants to understand why the code crashes — that is `debug-coach`.

## Prohibitions

- Do not change files and do not run commands that change them.
- Do not "improve" or rewrite the code until the student asks.
- Do not give a lecture on the topic away from this code: explain what is written in the file.
- Do not explain the obvious (imports, brackets) unless the student asks.

## Process

1. Identify the stack: the project files (`package.json`, `go.mod`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `*.csproj`, etc.) and the README. No project files — take the language from the file extension.
2. Identify the fragment: the file and lines the student is asking about. Not specified — take the selected or mentioned code; a large file (more than ~60 lines) — suggest starting with the main function and ask one question about which part to start with.
3. Read the code and what it calls in the project — to explain why it is needed, not only what it does.
4. Choose the mode:
   - **brief** (default) — split the code into meaningful blocks, for each: what it does and why;
   - **line by line** — only if the student asks ("line by line", "in detail", "every line"): one line or a pair of lines at a time; long code — in chunks of up to ~15 lines, then ask whether to continue.
5. Point out one non-obvious place: a trap, a side effect, or something people often get wrong.
6. Check where the code came from. If this code was written by AI in this session (you yourself at the "solution" step, at the student's request, or generated in another way), finish with a request for the student to explain the code in their own words instead of the usual question.

## Response format

Briefly:

```
**What it does overall:** <1 line>

- `lines 1–4` — <what and why>
- `lines 5–12` — …
- `lines 13–15` — …

**Watch out:** `line N` — <non-obvious place>

**Question:** <one comprehension question>
```

Line by line — the same format, but one bullet per line or pair of lines.

- Up to 15 lines of text, code quotes not counted.
- Line numbers refer to the student's file, as `path/to/file:line`.

## When to finish

- After the explanation — one comprehension question: what would change if a specific line were removed or altered, or what the result would be for a specific input.
- The code was written by AI in this session — instead, ask: "Explain in your own words what this code does and why line N is needed."
- The student has answered — say whether it is correct and correct it in 1–2 lines if not. Do not ask new questions.

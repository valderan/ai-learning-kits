---
name: topic-lesson
description: Explanation of a course topic with lesson notes, comprehension questions and self-study tasks. Use on phrases like "explain the topic", "tell me about …", "I want to understand the topic", "I need the theory of …", "make notes", "give me check questions", "give me practice tasks", "I want to practice the topic".
metadata:
  version: "1"
---

# topic-lesson — topic, notes, questions, tasks

## When to use

- The student wants to understand a topic: "explain the topic", "tell me about <technology>", "I want to understand …", "I need the theory of …".
- The student asks for notes: "make notes", "write up the topic", "save the material".
- The student asks to check understanding: "give me check questions", "test whether I got the topic".
- The student asks for practice: "give me practice tasks", "I want to practice the topic", "make some exercises".
- The student brings materials on the topic: links, files, text.

Not this skill: "explain this code" — `explain-code`; "I don't understand how to solve the task" — `hint-ladder`; "what's next in the program" — `course-plan`.

## Prohibitions

- Do not offer notes, questions or tasks on your own — only on the student's direct request. If `COURSE.md` says "Practice: tasks from a mentor", create tasks only after checking: "The course tasks come from your mentor. Shall I make extra ones?"
- Do not get ahead of the program: explain and create tasks only on the current topic and what has already been completed. Future topics — briefly "that will be in topic N".
- Do not invent facts, versions or links. No access to fresh sources — say so honestly and mark what the student should verify themselves.
- Do not solve tasks for the student: tasks are for their practice. If they ask for a solution — work through `hint-ladder`.
- Do not overwrite existing `notes/<NN>.md` and `tasks/<NN>.md`: read and extend them, naming the changes.
- Do not turn the lesson into a lecture in the chat: the full material goes into the notes file, the chat gets a short summary.
- Do not ask more than one question per answer, except for the block of comprehension questions (3–5) and the question about tasks.

## Process

1. **Topic.** Determine the current topic from `COURSE.md` and `COURSE_PROGRESS.md`; if the student named their own, work with it. If it is unclear which topic is meant, ask one question.
2. **Material and freshness.** Source order:
   1. the student's materials — links, files, pasted text: read them and build on them;
   2. a documentation MCP server, if connected (for example, context7) — take the current documentation for the technology in the version used by the project;
   3. web search — 1–3 queries against official documentation, releases, roadmap;
   4. nothing available — say so plainly and build on the course materials, marking places for the student to verify themselves.
   Take the technology version from the project (`package.json`, `go.mod`, `pyproject.toml`, `Cargo.toml`, etc.).
3. **Notes.** Build them in this structure: why the topic matters → key concepts → how it works (with examples) → common mistakes → cheat sheet → sources. Save to `notes/<NN>.md` (NN is the topic number; if the topic is not in the program, use the next free number). Extend an existing file instead of overwriting it. The chat gets 5–10 lines of the essence and the file path.
4. **Comprehension questions.** 3–5 questions from simple to hard, without answers. Wait for the student's answers.
5. **Review.** Check the answers, correct 1–2 lines per mistake, note what has been learned.
6. **Tasks.** Ask: "Do you want to reinforce the topic with tasks?" After agreement — 3–5 tasks from simple to hard:
   - 2–3 on the current topic, 1–2 on what has already been completed (from `COURSE_PROGRESS.md` and `notes/`);
   - difficulty according to the "Student context" in `COURSE.md`; nothing from future topics;
   - for each: difficulty level, task statement, acceptance check;
   - save to `tasks/<NN>.md`, put the list and the file path in the chat;
   - do not write solutions into the file.
7. **Finish.** Suggest starting with the first task. Remind the student that the topic can be closed on request ("close the topic").

## Response format

- Notes: full version in the file; the chat gets "**Notes:** `notes/02.md`" plus 5–10 lines of the essence.
- Questions: a numbered list of 3–5, no answers.
- Tasks: a list of 3–5 with a difficulty label and the link to completed topics; briefly in the chat.
- File references: `notes/02.md`, `tasks/02.md`; code references — `path/to/file:line`.
- Sources — in the "Sources" section of the notes, with links.

## When to finish

- The student has answered the questions, received the review and the tasks — stop and suggest starting with the first task.
- The student declined the tasks — finish after reviewing the answers.
- The student asks to close the topic — remind them to say "close the topic"; that is handled by `course-plan`.

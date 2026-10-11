---
name: course-plan
description: Working with the course program in the project — parse a ready-made program into COURSE.md and COURSE_PROGRESS.md, design a course from scratch for the student's goal with a check of current trends, update the program, close a completed topic. Use on phrases like "here is my program", "parse my program", "create COURSE.md", "make me a course plan", "I want to learn …", "what's next in the program", "update the program", "check if it's up to date", "close the topic", "mark the topic as done".
metadata:
  version: "1"
---

# course-plan — the course program

## When to use

- The student brings a study program in any form: text in the chat, a file in the project, a list, a link, a picture.
- The student wants to learn from scratch: "I want to learn NestJS", "make me a course on algorithms" — and there are no course files yet.
- The project already has `COURSE.md`/`COURSE_PROGRESS.md`, and the student asks to update the program or check whether it is up to date.
- The student directly asks to close a topic: "close the topic", "mark that I have finished".

If the student is just learning and asking about code — this is not the skill to use; use `hint-ladder`, `debug-coach`, `code-review` or `explain-code`.

## Prohibitions

- Do not create or rewrite `COURSE.md`/`COURSE_PROGRESS.md` without the student's explicit confirmation: first show a draft in the chat.
- Do not renumber topics and do not change the wording of topics already marked `[x]` — otherwise the progress breaks. Add new topics only at the end of a module and with new numbers.
- Do not delete topics from the program yourself: only suggest deleting them and explain why.
- Do not close a topic until the student directly asks. If it is unclear which topic they mean, ask one clarifying question.
- Do not invent trends and library versions: do not state anything without a confirmed source; if there is no web access, say so honestly.
- Do not make a course "about everything": the student's goal and "Out of scope" matter more than a complete list.
- Do not turn course design into a lecture: the course is files and a short presentation, not theory in the chat.
- Do not mix course design with teaching: after the files are created, return to the normal mentor mode.

## Process

1. Check the project root: whether `COURSE.md` and `COURSE_PROGRESS.md` exist. Then follow scenario A, B, C or D. Format examples are in `.agents/templates/`.

### A. A ready-made program

1. Read the program from any source: text in the chat, a project file, a link (if there is web access), a picture (if it can be read). If the source is unavailable — ask for it as text.
2. Normalize it into our format: modules as `###` headings, topics as a numbered list, short wording; remove duplicates and overlaps, keep the author's names if they are clear.
3. Check against current trends if there is web search: 1–3 queries, only official documentation, releases, roadmaps. What is outdated and what is missing for the student's goal — present as a list of suggested changes with reasons. No web search — say so plainly and give the student a short list of questions/sources to check themselves.
4. Build the header: "Learning goal", "Student context" (including the line `Practice: tasks from a mentor` or `Practice: self-study`), "What you will be able to do", "Out of scope", "When a topic counts as done". Ask who provides the tasks in one question if it is not stated. Do not re-ask anything else.
5. Show the draft in the chat: the header, the module structure and 2–5 suggested changes. Wait for confirmation.
6. Create `COURSE.md` and `COURSE_PROGRESS.md`: all topics `[ ]`, `Current: 1. First topic`, and at the bottom — `Updated: <date>` (and sources, if trends were checked).

### B. A course from scratch

1. Clarify in one turn, at most 4–5 short questions: the current level in the topic; why they are learning it (work, interview, pet project, for themselves); direction/specialization; time and pace; who provides the tasks — a mentor or should I invent them. Do not ask what the student has already said.
2. Research trends if there is web search: official documentation, releases, roadmap, reliable reviews. Collect the stack, versions and typical pitfalls. No web search — say so plainly and suggest sources for self-checking.
3. Offer 2–3 learning vectors for different goals. For each: who it suits, what you will be able to do at the end, modules (5–8 items), stack and libraries, what is out of scope, an approximate length in topics. Remember that one language has different vectors: Python — web, LLM, data; NestJS — REST, microservices, GraphQL.
4. Let the student choose or mix. "You decide" — pick according to their goal and explain the choice in one sentence.
5. After the choice, assemble the full `COURSE.md` in the format (with the `Updated: <date>` line) and create `COURSE_PROGRESS.md`.

### C. Program revision

1. Read `COURSE.md`, `COURSE_PROGRESS.md` and the date in the "Updated" line.
2. Check trends if there is web search.
3. Suggest changes: add topics and modules, update the stack and materials. New topics go at the end of a module with new numbers; do not touch completed ones.
4. After confirmation, update `COURSE.md`, add the new topics to `COURSE_PROGRESS.md` as `[ ]` and refresh the "Updated" date.

### D. Closing a topic

1. Read `COURSE_PROGRESS.md` and find the student's topic.
2. Mark it `[x]`, move `Current` to the next item without a mark; if all are marked — `Current: course completed`.
3. Say what you changed and suggest the next topic.

## Response format

- Course design (B): up to ~40 lines of structured text for all variants; variants as lists, without fluff.
- Parsing a program (A) and revision (C): the header + modules + a list of changes with reasons, also compact.
- Creating and editing files (A, B, C, D): a short report — which files were created or changed and what changed in them.
- Reference files as `COURSE.md:12`.
- One question per answer, except the interview in B: there it is one block of 4–5 questions.
- List the sources you relied on as links in the "Materials" section of `COURSE.md`.

## When to finish

- The files are created or updated and the student has confirmed the result — briefly say what is next: suggest opening topic 1 (or the current one) and return to the normal mentor mode.
- In scenario D, name the next topic and stop.
- If the student declined the changes — leave the files as they are and return to teaching.

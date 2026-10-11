# Learning mode for OpenCode 2.x — student guide

This folder turns OpenCode into a mentor: the agent hints, reviews and explains, but you write the code. The mode is **on right away**: the `student` agent is set as the primary one in the project, so there is nothing to choose.

## What is inside

| File | Purpose |
|---|---|
| `opencode.json` | Project config: `"default_agent": "student"` — the agent becomes primary on start |
| `agents/student.md` | The mentor persona and permissions (`permissions`): edits — with confirmation, tests and the course program — without |
| `skills/` | Six skills the agent picks up as needed |
| `templates/` | Example `COURSE.md` and `COURSE_PROGRESS.md` for Go, Python, TypeScript and CSS |
| `README.md` | This file |

## Quick start

1. Copy the `.opencode` folder into the root of your learning project.
2. Run `opencode` in that project — the `student` agent is already primary.
3. You can see the agent list and switch with Shift+Tab (Tab in V1), but for learning there is nothing to switch.

If OpenCode was already running and the skills are not visible, restart the background service: `opencode service restart`. The service indexes skills and agents at start and does not notice new ones; `opencode reload` does not help here.

## Course program and progress

The project root may contain two optional files:

```
COURSE.md           # what and why we learn: goal, context, modules and topics, materials
COURSE_PROGRESS.md  # the "Current: N. Topic" line and the checklist of what is done
```

The agent reads them at the start of the session and keeps hints within the current topic, without getting ahead. If the files are missing, it offers once to create them and does not insist.

Three ways to set up the course files:

1. **Give the program to the agent.** Say: "here is my study program" and send it as text, a file or a link. The agent parses it, checks how current it is against official sources (if web search is available), shows a draft and creates the files.
2. **Ask for a course from scratch.** Say: "I want to learn NestJS". The agent first asks about your level, goal and time, then offers 2–3 learning vectors — and after your choice creates the files.
3. **Take a ready example.** Copy `.opencode/templates/<language>/COURSE.md` and `COURSE_PROGRESS.md` into the project root and replace the topics with your own.

### Notes and tasks

- `notes/<NN>.md` — lesson notes: the agent creates them on request ("explain the topic" or "make notes").
- `tasks/<NN>.md` — self-study tasks: 3–5, from simple to hard, only on the current and already completed topics.
- The agent does not offer notes or tasks on its own — only on your request. If `COURSE.md` says "Practice: tasks from a mentor", the course tasks come from your mentor, and the agent will only create extra ones after checking first.

How progress works:

```markdown
Current: 2. Functions

- [x] 1. Variables and types
- [ ] 2. Functions
- [ ] 3. map and filter
```

- The current topic comes from the `Current` line; if it is absent — the first item without `[x]`.
- A topic is closed by the agent, but **only on your direct request**: "close the topic", "mark that I finished". It sets `[x]` and moves `Current` to the next item.
- The program can be updated at any time: "update the program", "check if it's up to date". The agent suggests changes; completed topics stay untouched.

## Skills

The agent picks them up itself by the situation. In V2 the skill list is under `ctrl+p → Skills`; you can invoke one manually as `/skill:<id>` if skill commands are enabled in your build.

| Skill | When it triggers |
|---|---|
| `hint-ladder` | "I'm stuck", "it doesn't work", "I don't know what's next" — hints in steps, from a direction to the finished solution |
| `code-review` | "review my code", "what's wrong with the solution" — a review without rewriting |
| `debug-coach` | an error, a stack trace, "it crashes", "wrong output" — working through the error without a ready-made fix |
| `explain-code` | "explain this code", "what's going on here" — explanation by blocks or line by line |
| `course-plan` | the course program: parse a program, build a course, update it, close a topic |
| `topic-lesson` | "explain the topic", "make notes", "give me check questions", "give me practice tasks" — notes in `notes/`, tasks in `tasks/` |

After adding or editing skills, restart the service: `opencode service restart`.

## Action confirmations

The permissions are set in `agents/student.md` as a `permissions` list:

- reading the project — free;
- file edits and writes — with confirmation;
- running tests and the course program (`npm test`, `node`, `python`, `pytest`, `go test`, `cargo test`, etc.) — without confirmation;
- other commands and unfamiliar skills — with confirmation.

Do not ask the agent to bypass confirmations. To change the rules, edit the `permissions` list in `agents/student.md` and restart the service.

## Checking that the mode works

- Type "I'm stuck" — the agent should give "Hint 1 of 4" without ready-made code.
- Type "review my code" — you get a review with `file:line` references, without a rewritten solution.
- If your build has the debug commands: `opencode debug config` (should show `default_agent: student`) and `opencode debug skill` (the kit's six skills).
- At the start of a session in a project with `COURSE.md`, the transcript should show reads of `COURSE.md` and `COURSE_PROGRESS.md` — before the first answer.

## If something is wrong

| Symptom | What to do |
|---|---|
| The agent behaves like a regular assistant | Check `default_agent` in `opencode.json`; run opencode from the project root |
| Skills did not appear after copying | `opencode service restart`, then `ctrl+p → Skills` |
| The agent did not refer to the program | Say "read COURSE.md and COURSE_PROGRESS.md" |
| Progress is not marked without a request | That is by design: say "close the topic" |
| I want the normal mode | Remove `"default_agent": "student"` from `opencode.json` — the agent stays available via Shift+Tab |

## Turning the mode off completely

- Remove `"default_agent": "student"` from `.opencode/opencode.json` — the mode stops being primary, the agent stays in the list.
- Rename or delete `.opencode/agents/student.md` — the agent disappears.
- Remove the `.opencode` folder from the project — everything is off.

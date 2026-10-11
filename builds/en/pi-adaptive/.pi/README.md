# Learning mode for pi — student guide

This folder turns pi into a mentor: the agent hints, reviews and explains, but you write the code. The mode is **always on** while `.pi/APPEND_SYSTEM.md` is in the project — there is nothing to enable.

## What is inside

| File | Purpose |
|---|---|
| `APPEND_SYSTEM.md` | The mentor persona. pi adds it to the system prompt on every start — that is why the mode works from the first message |
| `skills/` | Six skills the agent loads as needed |
| `templates/` | Example `COURSE.md` and `COURSE_PROGRESS.md` for Go, Python, TypeScript and CSS |
| `settings.json` | `pi-guard` rules for this project; guard itself is enabled and disabled globally |
| `README.md` | This file |

## Quick start

1. Copy the `.pi` folder into the root of your learning project.
2. Run `pi` in that project.
3. On the first run pi asks whether to trust the project files — answer yes. Without trust `.pi` is not loaded: this is pi's protection against foreign configs.
4. Check that the mode works: ask "who are you?" — the agent will answer as a mentor and will not start writing code for you.

Useful to know:

- `/trust` — remember the trust decision for this folder, so it stops asking. A decision for a parent folder (for example `~/learning`) covers all nested projects.
- `pi --approve` — trust for one run.
- `pi --no-approve` — run pi **without** the learning mode (project `.pi` files are ignored).
- If you copy `.pi` into an already running session — run `/reload`.

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
3. **Take a ready example.** Copy `.pi/templates/<language>/COURSE.md` and `COURSE_PROGRESS.md` into the project root and replace the topics with your own.

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

The agent picks them up itself by the situation. You can invoke one manually: `/skill:<id>`.

| Skill | When it triggers |
|---|---|
| `hint-ladder` | "I'm stuck", "it doesn't work", "I don't know what's next" — hints in steps, from a direction to the finished solution |
| `code-review` | "review my code", "what's wrong with the solution" — a review without rewriting |
| `debug-coach` | an error, a stack trace, "it crashes", "wrong output" — working through the error without a ready-made fix |
| `explain-code` | "explain this code", "what's going on here" — explanation by blocks or line by line |
| `course-plan` | the course program: parse a program, build a course, update it, close a topic |
| `topic-lesson` | "explain the topic", "make notes", "give me check questions", "give me practice tasks" — notes in `notes/`, tasks in `tasks/` |

## Action confirmations

The state of guard is a **global pi-guard setting** (stored in `~/.pi/agent/settings.json`), while `.pi/settings.json` only provides the rules for the learning project: edits and writes — with confirmation, tests and the course program — without.

- `/guard list` — see the current state and rules;
- `/guard enable` — turn confirmations on, `/guard disable` — off, `/guard toggle` — switch.

Free mode (pi asks nothing): `/guard disable`. Then the "you write the code" rule is held only by the mentor persona. If pi-guard is installed and its global settings are empty, it is enabled by default — so start with `/guard list` and choose the mode yourself.

What changes with guard enabled:

- file edits and writes — with confirmation;
- running tests and the course program (`npm test`, `node`, `python`, `pytest`, `go test`, `cargo test`, etc.) — without confirmation;
- reading — without confirmation;
- other commands — with confirmation.

The rules only work if the `pi-guard` extension is installed: `pi install npm:pi-guard`. Without it `settings.json` is simply ignored — and everything else in the kit keeps working.

## Checking that the mode works

- Type "I'm stuck" — the agent should load `hint-ladder` and give "Hint 1 of 4" without ready-made code.
- Type "review my code" — you get a review with `file:line` references, without a rewritten solution.
- Open `/` and make sure the list contains `/skill:hint-ladder`, `/skill:code-review`, `/skill:debug-coach`, `/skill:explain-code`, `/skill:course-plan`, `/skill:topic-lesson`.
- At the start of a session in a project with `COURSE.md`, the transcript should show reads of `COURSE.md` and `COURSE_PROGRESS.md` — before the first answer.

## If something is wrong

| Symptom | What to do |
|---|---|
| The agent behaves like a regular assistant | Check that the mode is on: run pi without `--no-approve` and confirm trust; then `/reload` |
| No `/skill:...` commands | Make sure the whole `.pi/skills` folder was copied and the project trust was granted |
| The agent did not refer to the program | Say "read COURSE.md and COURSE_PROGRESS.md" |
| Progress is not marked without a request | That is by design: say "close the topic" |
| I want the normal mode | `pi --no-approve`, or `/guard disable`, or remove `.pi/APPEND_SYSTEM.md` (rename it to bring it back) |

## Turning the mode off completely

- For one run: `pi --no-approve`.
- Permanently in this project: delete or rename `.pi/APPEND_SYSTEM.md` — the persona disappears, the skills stay available.
- Completely: remove the `.pi` folder from the project.

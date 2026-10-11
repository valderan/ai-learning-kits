# Learning mode — student guide

This kit turns an agent into a mentor: it hints, reviews and explains, but you write the code. The mode is **always on** while `AGENTS.md` with these instructions is in the project root — there is nothing to enable.

## How the kit is put together

| What | Where | Purpose |
|---|---|---|
| Mentor persona | `AGENTS.md` in the project root | The agent's main session reads this file at start — that is why the mode works from the first message |
| Skills | `.agents/skills/<id>/SKILL.md` | Six skills the agent picks up as needed |
| Course templates | `.agents/templates/<language>/` | Example `COURSE.md` and `COURSE_PROGRESS.md` for Go, Python, TypeScript and CSS |
| This guide | `.agents/README.md` | For you; the agent does not read it |

## Quick start

1. Copy `AGENTS.md` and the `.agents` folder into the root of your learning project.
2. If the project already had its own `AGENTS.md` — do not overwrite it, append the mentor instructions to the end.
3. Run the agent in that project — the mode is already active.

Special cases:

- **Claude Code**: if the project has a `CLAUDE.md`, it overrides `AGENTS.md` — append the mentor instructions to `CLAUDE.md` (or delete it if you do not need it). Claude Code takes skills from `.claude/skills`, so add a link: `mkdir -p .claude && ln -s ../.agents/skills .claude/skills`.
- Other agents that do not read `AGENTS.md` — check their instructions file and copy the contents of `AGENTS.md` there.
- Some agents (for example, pi) ask for permission to read project files on the first run — answer yes, otherwise the skills will not load.

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
3. **Take a ready example.** Copy `.agents/templates/<language>/COURSE.md` and `COURSE_PROGRESS.md` into the project root and replace the topics with your own.

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

In agents with skill support they are picked up automatically by the situation. If you can invoke them manually, try `/skill:<id>`.

| Skill | When it triggers |
|---|---|
| `hint-ladder` | "I'm stuck", "it doesn't work", "I don't know what's next" — hints in steps, from a direction to the finished solution |
| `code-review` | "review my code", "what's wrong with the solution" — a review without rewriting |
| `debug-coach` | an error, a stack trace, "it crashes", "wrong output" — working through the error without a ready-made fix |
| `explain-code` | "explain this code", "what's going on here" — explanation by blocks or line by line |
| `course-plan` | the course program: parse a program, build a course, update it, close a topic |
| `topic-lesson` | "explain the topic", "make notes", "give me check questions", "give me practice tasks" — notes in `notes/`, tasks in `tasks/` |

If the agent did not pick up a skill itself — say directly: "read `.agents/skills/hint-ladder/SKILL.md` and act according to it".

## Action confirmations

The kit does not configure permissions: every agent has its own mechanism, and that is fine. If confirmations are enabled — approve or reject the agent's actions, but do not ask it to bypass the protection. If you want tight control, see the kit README: it collects recipes for pi, Claude Code, Codex and OpenCode.

The main "you write the code" rule is held by the mentor persona itself, not by permission settings.

## Checking that the mode works

- Type "I'm stuck" — the agent should give "Hint 1 of 4" without ready-made code.
- Type "review my code" — you get a review with `file:line` references, without a rewritten solution.
- At the start of a session in a project with `COURSE.md`, the transcript should show reads of `COURSE.md` and `COURSE_PROGRESS.md` — before the first answer.

## If something is wrong

| Symptom | What to do |
|---|---|
| The agent behaves like a regular assistant | Check that `AGENTS.md` is in the project root and the agent reads it (with Claude Code — that no `CLAUDE.md` overrides it) |
| The agent did not refer to the program | Say "read COURSE.md and COURSE_PROGRESS.md" |
| Progress is not marked without a request | That is by design: say "close the topic" |
| Skills are not found | Say "read `.agents/skills/<id>/SKILL.md`"; with pi, check the project trust confirmation |
| I want the normal mode | Rename or delete `AGENTS.md` (put it back when you need it again) |

## Turning the mode off completely

- For a while: rename `AGENTS.md` to `AGENTS.md.off` — the persona disappears, the skills stay available.
- Permanently: delete `AGENTS.md` and the `.agents` folder from the project.

# ai-learning-kits

Learning-mode kits for AI coding agents: a mentor that hints, reviews and explains, while the student writes the code. No global install — copy a kit into your learning project and it is picked up on start.

## Kits

| Kit | For | Install |
|---|---|---|
| [pi-adaptive](builds/ru/pi-adaptive/README.md) | pi | `cp -R builds/ru/pi-adaptive/.pi <project>/` |
| [all-adaptive](builds/ru/all-adaptive/README.md) | agents that read `AGENTS.md` and `.agents/skills/`: Codex, Cursor, Gemini CLI, Copilot/VS Code, OpenCode, pi | `cp builds/ru/all-adaptive/AGENTS.md <project>/` and `cp -R builds/ru/all-adaptive/.agents <project>/` |
| [opencode-adaptive](builds/ru/opencode-adaptive/README.md) | OpenCode 1.x (v1) and 2.x (v2) | `cp -R builds/ru/opencode-adaptive/v1/.opencode <project>/` |

Kit documentation is in Russian for now; English builds are planned in `builds/en/`.

## What the mentor does

- **Hints, reviews, debugging, code explanation** — `hint-ladder`, `code-review`, `debug-coach`, `explain-code`: minimal help, no ready-made solutions.
- **Course program** — `COURSE.md` and `COURSE_PROGRESS.md` in the project root: topics, current topic, marking progress on request (`course-plan`).
- **Topic lessons** — notes in `notes/<NN>.md`, comprehension questions, self-study tasks in `tasks/<NN>.md` (`topic-lesson`).
- **Tasks only on request**: if `COURSE.md` says "Практика: задачи от наставника", the agent does not push its own exercises.

## Layout

```
ai-learning-kits/
├── AGENTS.md          # instructions for agents working on this project
├── README.md          # Russian version
├── README_en.md       # this file
├── LICENSE
└── builds/
    └── ru/
        ├── pi-adaptive/
        ├── all-adaptive/
        └── opencode-adaptive/
```

Planned: English builds in `builds/en/` and a Python installer for macOS, Linux and Windows.

## Requirements

- pi, OpenCode, or any agent that reads `AGENTS.md` / `.agents/skills`.
- For action confirmations in pi — the `pi-guard` extension (optional).

## License

MIT — see [LICENSE](LICENSE).

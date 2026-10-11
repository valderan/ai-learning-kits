# all-adaptive — learning mode for any agent

Learning mode for general agent standards: **AGENTS.md** for the main session instructions and **`.agents/skills/`** for skills. The mentor hints, reviews and explains, but **the student writes the code**.

Difference from [pi-adaptive](../pi-adaptive/README.md): nothing here is tied to a specific harness — no `.pi`, no `pi-guard`, no project trust. Just two portable artefacts: `AGENTS.md` and the `.agents` folder.

## Contents

```
all-adaptive/
├── README.md                # this file
├── AGENTS.md                # the mentor persona → copied to the project root
└── .agents/
    ├── README.md            # detailed guide for the student
    ├── skills/              # 6 skills (Agent Skills spec)
    │   ├── hint-ladder/     # step-by-step hints
    │   ├── code-review/     # review of the solution
    │   ├── debug-coach/     # working through an error
    │   ├── explain-code/    # explaining code
    │   ├── course-plan/     # the course program and progress
    │   └── topic-lesson/    # topic: notes, questions, tasks
    └── templates/           # examples of COURSE.md + COURSE_PROGRESS.md
        ├── go/  python/  typescript/  css/
```

## Installation

```bash
cp builds/en/all-adaptive/AGENTS.md /path/to/learning/project/
cp -R builds/en/all-adaptive/.agents /path/to/learning/project/
```

If the project **already has** an `AGENTS.md` — do not overwrite it, append the kit to the end:

```bash
printf '\n\n' >> /path/to/project/AGENTS.md
cat builds/en/all-adaptive/AGENTS.md >> /path/to/project/AGENTS.md
```

Then just run the agent in the project — the mode works from the first message.

## Compatibility

| Agent | Reads `AGENTS.md` | Reads `.agents/skills/` |
|---|---|---|
| OpenAI Codex | yes | yes (its native directory) |
| Cursor | yes | yes |
| Gemini CLI | yes | yes (takes priority over `.gemini/skills`) |
| VS Code / Copilot | yes | yes (along with `.github/skills`, `.claude/skills`) |
| OpenCode | yes | yes |
| pi | yes | yes (project trust must be confirmed) |
| Windsurf, Kiro, Antigravity and others | yes | yes |
| **Claude Code** | ⚠️ only if the project has no `CLAUDE.md` (since 2.1.277) | ❌ — reads only `.claude/skills` |

Claude Code specifics:

- if a `CLAUDE.md` already exists, it overrides `AGENTS.md` — append the persona to `CLAUDE.md`;
- link the skills:
  ```bash
  mkdir -p .claude && ln -s ../.agents/skills .claude/skills
  ```

Note for pi: `.agents/templates/*.md` do not interfere with `pi-subagents` — files without `name`/`description` frontmatter are silently skipped there.

## Dependencies

None. No extensions, no plugins, no settings: only markdown files.

## Action confirmations (optional)

There is no single permission standard across agents, so the kit does not configure them itself. The behavioural rules ("do not edit files without an explicit request", "do not bypass confirmations") are already in `AGENTS.md`. If you need tight control, enable your agent's built-in mechanism:

- **pi** — the `pi-guard` extension: put the rules in `.pi/settings.json` (only the rules are read from the project file, while `enabled` is a global setting in `~/.pi/agent/settings.json`): edits and writes — `ask`, tests and reading — `allow`; enable with `/guard enable`. A ready example is in `builds/en/pi-adaptive/.pi/settings.json`.
- **Claude Code** — `permissions` in `.claude/settings.json` (rules like `Bash(npm test:*)`, `Edit`); check the syntax in the docs for your version.
- **Codex** — `approval_policy` and `sandbox_mode` in the config (`~/.codex/config.toml`).
- **OpenCode** — the `permission` block in the agent description: an example is in the [`opencode-adaptive`](../opencode-adaptive/v1/.opencode/agents/student.md) build.
- **Cursor, Copilot, Gemini CLI** — built-in tool confirmations, enabled in the settings.

## Verification

1. Copy `AGENTS.md` and `.agents` into a test project, run the agent.
2. Type "I'm stuck" → the answer "Hint 1 of 4", without ready-made code.
3. In a project with `COURSE.md`, at the start of the session you can see reads of `COURSE.md` and `COURSE_PROGRESS.md`.
4. Say "I want to learn <technology>" → the agent asks clarifying questions and offers 2–3 course vectors instead of writing files right away.

## Limitations

- `AGENTS.md` is not a system prompt but project context: its weight and priority depend on the agent, though most harnesses read it at start.
- Skills still work in a harness without skill support: the persona asks the agent to read `.agents/skills/<id>/SKILL.md`.
- Reading `COURSE.md` is a model action per instruction, not a hook.
- With Claude Code there are manual steps (see "Claude Code specifics"); the kit does not try to automate them.

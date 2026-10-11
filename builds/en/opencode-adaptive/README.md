# opencode-adaptive — learning mode for OpenCode without a global install

Learning mode for a project-local OpenCode setup: the `student` agent and six skills live in `.opencode/` inside the learning project and are picked up on start. The agent is primary right away — no manual selection needed. Nothing in `~/.config/opencode` is touched, no global install required.

Two complete builds: **v1** and **v2** — for the respective OpenCode versions. Each is self-contained: copy one folder and go.

## Which version to choose

```bash
opencode --version
```

- major **1** (for example, `1.18.35`) → `v1`;
- major **2** and above → `v2`.

Automatically:

```bash
V=$(opencode --version | sed -n 's/^[^0-9]*\([0-9][0-9]*\)\..*/\1/p')
[ "$V" -ge 2 ] && DIR=v2 || DIR=v1
cp -R builds/en/opencode-adaptive/$DIR/.opencode /path/to/learning/project/
```

## Contents

```
opencode-adaptive/
├── README.md                # this file
├── v1/.opencode/            # complete build for OpenCode 1.x
│   ├── opencode.json        # { "$schema": …, "default_agent": "student" }
│   ├── agents/student.md    # V1 format: permission (object)
│   ├── skills/              # 6 skills
│   ├── templates/           # go, python, typescript, css
│   └── README.md            # student guide
└── v2/.opencode/            # complete build for OpenCode 2.x
    ├── opencode.json        # the same
    ├── agents/student.md    # V2 format: permissions (list)
    ├── skills/              # the same 6 skills
    ├── templates/           # the same 8 templates
    └── README.md            # student guide + V2 specifics
```

Inside each build:

- **the `student` agent** — a brand-neutral mentor persona with the course program logic; permissions: edits — with confirmation, tests and the course program — without;
- **6 skills**: `hint-ladder`, `code-review`, `debug-coach`, `explain-code`, `course-plan`, `topic-lesson`;
- **8 templates**: `COURSE.md` + `COURSE_PROGRESS.md` for Go, Python, TypeScript and CSS;
- **`opencode.json`** with `"default_agent": "student"` — the mode is on right away.

## Installation

```bash
cp -R builds/en/opencode-adaptive/v1/.opencode /path/to/learning/project/   # for OpenCode 1.x
cp -R builds/en/opencode-adaptive/v2/.opencode /path/to/learning/project/   # for OpenCode 2.x
```

Then run `opencode` from the project root. If the OpenCode 2 service was already running and the skills are not visible: `opencode service restart` (`opencode reload` does not help).

## How the versions differ

| | v1 | v2 |
|---|---|---|
| Agent frontmatter | `permission` (an object of rules) | `permissions` (an ordered list of `action`/`resource`/`effect`) |
| Persona body | identical | identical |
| Skills and templates | the same | the same |
| Skills in the interface | via `/skill:<id>` | `ctrl+p → Skills`; in 2.0.15 skills may not appear in the `/` menu |
| Updating after copying | restarting opencode is enough | `opencode service restart` |

## Verification

```bash
cd /path/to/learning/project
opencode debug config        # default_agent: student
opencode debug agent student # agent rules: edit → ask, npm test/go test → allow
opencode debug skill         # the kit's six skills with .opencode/skills/... paths
```

In a session:

- "I'm stuck" → the answer "Hint 1 of 4" without ready-made code;
- in a project with `COURSE.md`, at the start of the session you can see reads of `COURSE.md` and `COURSE_PROGRESS.md`;
- "I want to learn <technology>" → the agent asks clarifying questions and offers 2–3 course vectors instead of writing files right away.

## Differences from the other builds

- **[pi-adaptive](../pi-adaptive/README.md)** — for pi: the persona in `.pi/APPEND_SYSTEM.md`, permissions via `pi-guard`.
- **[all-adaptive](../all-adaptive/README.md)** — the general standard: `AGENTS.md` + `.agents/skills`.

## Turning off

- Remove `"default_agent": "student"` from `.opencode/opencode.json` — the mode stops being primary, the agent stays in the list (Tab/Shift+Tab).
- Rename or delete `.opencode/agents/student.md` — the agent disappears.
- Remove `.opencode` from the project — turn everything off.

## Limitations

- The v1 and v2 builds are not synchronised automatically: skills and templates are copies, so when editing the persona you have to change it in both.
- Reading `COURSE.md` is a model action per the persona instruction, not an OpenCode mechanism.
- Checking how current the program is depends on the agent's web access: without it the agent will say so honestly and suggest sources to check yourself.
- If the global `~/.config/opencode/opencode.json` already sets a different `default_agent`, the project config overrides it — that is expected.

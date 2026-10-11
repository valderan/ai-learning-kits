# pi-adaptive — learning mode for pi

Learning mode for pi: a mentor that hints, reviews and explains, but **the student writes the code**.

Differences from the OpenCode build:

- pi cannot switch session agents, so the persona lives in `.pi/APPEND_SYSTEM.md` and turns on as soon as pi starts in the project — there is no separate "primary agent" and no switch;
- pi does not ask for tool confirmations by default, so the OpenCode agent's permissions were moved into `pi-guard` **rules** in `.pi/settings.json` (edits — with confirmation, tests — without); guard itself is enabled and disabled globally: `/guard enable|disable|toggle`;
- the kit has no subagents, extensions or scripts — only static files;
- it is not synchronised with the OpenCode build and lives separately — a deliberate decision.

## Contents

```
pi-adaptive/
├── README.md                # this file
└── .pi/
    ├── README.md            # detailed guide for the student
    ├── APPEND_SYSTEM.md     # the mentor persona (turns on at start)
    ├── settings.json        # pi-guard rules for the learning project
    ├── skills/
    │   ├── hint-ladder/     # step-by-step hints
    │   ├── code-review/     # review of the solution
    │   ├── debug-coach/     # working through an error
    │   ├── explain-code/    # explaining code
    │   ├── course-plan/     # the course program and progress
    │   └── topic-lesson/    # topic: notes, questions, tasks
    └── templates/           # examples of COURSE.md + COURSE_PROGRESS.md
        ├── go/
        ├── python/
        ├── typescript/
        └── css/
```

## Installation

```bash
cp -R builds/en/pi-adaptive/.pi /path/to/learning/project/
cd /path/to/learning/project
pi
```

At the first start pi asks whether to trust the project files — `.pi/APPEND_SYSTEM.md` and `.pi/skills/` are protected resources. Answer yes and the mode is on. Useful options:

- `/trust` — remember the decision for the folder (a parent folder's decision covers nested projects);
- `pi --approve` — trust for one run;
- `pi --no-approve` — start **without** the learning mode;
- `defaultProjectTrust: "always"` in `~/.pi/agent/settings.json` — for a dedicated learning machine (not part of the kit, it is a global setting).

If the folder is copied into an already running session — `/reload`.

## Dependencies

- pi (project `.pi` resources are supported out of the box).
- `pi-guard` — **optional**, only for action confirmations: `pi install npm:pi-guard`. Without it the `guard` section in `settings.json` is ignored, everything else works.

## Turning off

- `pi --no-approve` — one run without the mode.
- Rename/delete `.pi/APPEND_SYSTEM.md` — turn off the persona, keep the skills.
- Delete `.pi` — turn everything off.

## Verification

Quick scenario (the detailed protocol is in `.pi/README.md`):

1. Copy `.pi` into a test project, run `pi --approve`, make sure the start output lists the skills.
2. "I'm stuck" → the agent answers "Hint 1 of 4" and does not write ready-made code.
3. In a project with `COURSE.md`, at the start of the session you can see reads of `COURSE.md` and `COURSE_PROGRESS.md` before the first answer.
4. `/guard list` → the current state and rules; `/guard enable` → an agent file edit asks for confirmation, `npm test` does not.

## Limitations

- The mode is always on in a project where `.pi/APPEND_SYSTEM.md` lives; it is not a switch but the learning project environment.
- Reading `COURSE.md` is a model action per instruction, not a pi hook: the agent does it on the first turn, but there is no extension-level guarantee.
- Checking how current the program is depends on pi's web access: without it the agent will say so honestly and suggest sources to check yourself.
- Without `pi-guard` the permissions are held only by the prompt: pi does not ask for confirmations by itself.

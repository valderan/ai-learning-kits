# ai-learning-kits

Наборы учебного режима для AI-агентов: наставник, который подсказывает, проверяет и объясняет, но **код пишет студент**. Никакой глобальной установки — сборка копируется в учебный проект и подхватывается при запуске.

## Сборки

| Сборка | Для кого | Установка |
|---|---|---|
| [pi-adaptive](builds/ru/pi-adaptive/README.md) | pi | `cp -R builds/ru/pi-adaptive/.pi <проект>/` |
| [all-adaptive](builds/ru/all-adaptive/README.md) | агенты, читающие `AGENTS.md` и `.agents/skills/`: Codex, Cursor, Gemini CLI, Copilot/VS Code, OpenCode, pi | `cp builds/ru/all-adaptive/AGENTS.md <проект>/` и `cp -R builds/ru/all-adaptive/.agents <проект>/` |
| [opencode-adaptive](builds/ru/opencode-adaptive/README.md) | OpenCode 1.x (v1) и 2.x (v2) | `cp -R builds/ru/opencode-adaptive/v1/.opencode <проект>/` |

## Что умеет наставник

- **Подсказки, ревью, отладка, объяснение кода** — `hint-ladder`, `code-review`, `debug-coach`, `explain-code`: минимальная помощь, без готовых решений.
- **Программа курса** — `COURSE.md` и `COURSE_PROGRESS.md` в корне проекта: темы, текущая тема, отметка пройденного по просьбе (`course-plan`).
- **Уроки по темам** — конспект в `notes/<NN>.md`, вопросы на усвоение, задачи для самоподготовки в `tasks/<NN>.md` (`topic-lesson`).
- **Задачи только по просьбе**: если в `COURSE.md` указано «Практика: задачи от наставника», агент не навязывает свои задания.

Подробности и настройка — в README каждой сборки; инструкция для студента лежит внутри сборки рядом с конфигами.

## Структура

```
ai-learning-kits/
├── AGENTS.md          # инструкции для агентов, работающих над проектом
├── README.md          # этот файл
├── README_en.md       # English version
├── LICENSE
└── builds/
    └── ru/
        ├── pi-adaptive/
        ├── all-adaptive/
        └── opencode-adaptive/
```

Планируется: английская версия сборок в `builds/en/` и инсталлятор на Python для macOS, Linux и Windows.

## Требования

- Один из агентов: pi, OpenCode или любой другой, читающий `AGENTS.md` / `.agents/skills`.
- Для подтверждений действий в pi — расширение `pi-guard` (опционально).

## Лицензия

MIT — см. [LICENSE](LICENSE).

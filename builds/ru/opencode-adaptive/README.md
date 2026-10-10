# opencode-adaptive — учебный режим для OpenCode без глобальной установки

Учебный режим для проектной установки OpenCode: агент `student` и шесть скиллов лежат в `.opencode/` внутри учебного проекта и подхватываются при запуске. Агент сразу основной — выбирать его вручную не нужно. Ничего в `~/.config/opencode` не трогается, глобальная установка не нужна.

Две полные сборки: **v1** и **v2** — под соответствующие версии OpenCode. Каждая самодостаточна: копируешь одну папку и работаешь.

## Какую версию выбрать

```bash
opencode --version
```

- major **1** (например, `1.18.35`) → `v1`;
- major **2** и выше → `v2`.

Автоматически:

```bash
V=$(opencode --version | sed -n 's/^[^0-9]*\([0-9][0-9]*\)\..*/\1/p')
[ "$V" -ge 2 ] && DIR=v2 || DIR=v1
cp -R builds/ru/opencode-adaptive/$DIR/.opencode /путь/к/учебному/проекту/
```

## Состав

```
opencode-adaptive/
├── README.md                # этот файл
├── v1/.opencode/            # полная сборка для OpenCode 1.x
│   ├── opencode.json        # { "$schema": …, "default_agent": "student" }
│   ├── agents/student.md    # формат V1: permission (объект)
│   ├── skills/              # 6 скиллов
│   ├── templates/           # go, python, typescript, css
│   └── README.md            # инструкция студенту
└── v2/.opencode/            # полная сборка для OpenCode 2.x
    ├── opencode.json        # то же
    ├── agents/student.md    # формат V2: permissions (список)
    ├── skills/              # те же 6 скиллов
    ├── templates/           # те же 8 шаблонов
    └── README.md            # инструкция студенту + нюансы V2
```

Внутри каждой сборки:

- **агент `student`** — обезличенная персона наставника с логикой программы курса; права: правки — с подтверждением, тесты и программа курса — без;
- **6 скиллов**: `hint-ladder`, `code-review`, `debug-coach`, `explain-code`, `course-plan`, `topic-lesson`;
- **8 шаблонов**: `COURSE.md` + `COURSE_PROGRESS.md` для Go, Python, TypeScript и CSS;
- **`opencode.json`** с `"default_agent": "student"` — режим включается сразу.

## Установка

```bash
cp -R builds/ru/opencode-adaptive/v1/.opencode /путь/к/учебному/проекту/   # для OpenCode 1.x
cp -R builds/ru/opencode-adaptive/v2/.opencode /путь/к/учебному/проекту/   # для OpenCode 2.x
```

Дальше — `opencode` из корня проекта. Если сервис OpenCode 2 уже был запущен и скиллы не видны: `opencode service restart` (`opencode reload` не помогает).

## Чем версии отличаются

| | v1 | v2 |
|---|---|---|
| Frontmatter агента | `permission` (объект правил) | `permissions` (упорядоченный список `action`/`resource`/`effect`) |
| Тело персоны | идентичное | идентичное |
| Скиллы и шаблоны | одинаковые | одинаковые |
| Скиллы в интерфейсе | через `/skill:<id>` | `ctrl+p → Skills`; в 2.0.15 скиллов может не быть в меню `/` |
| Обновление после копирования | достаточно перезапустить opencode | `opencode service restart` |

## Проверка

```bash
cd /путь/к/учебному/проекту
opencode debug config        # default_agent: student
opencode debug agent student # правила агента: edit → ask, npm test/go test → allow
opencode debug skill         # шесть скиллов набора с путями .opencode/skills/...
```

В сессии:

- «я застрял» → ответ «Подсказка 1 из 4» без готового кода;
- в проекте с `COURSE.md` — в начале сессии видны чтения `COURSE.md` и `COURSE_PROGRESS.md`;
- «хочу научиться <технология>» → агент задаёт уточняющие вопросы и предлагает 2–3 вектора курса, а не сразу пишет файлы.

## Отличия от других сборок

- **[pi-adaptive](../pi-adaptive/README.md)** — для pi: персона в `.pi/APPEND_SYSTEM.md`, права через `pi-guard`.
- **[all-adaptive](../all-adaptive/README.md)** — общий стандарт: `AGENTS.md` + `.agents/skills`.

## Отключение

- Убрать `"default_agent": "student"` из `.opencode/opencode.json` — режим перестанет быть основным, агент останется в списке (Tab/Shift+Tab).
- Переименовать или удалить `.opencode/agents/student.md` — агент исчезнет.
- Удалить `.opencode` из проекта — выключить всё.

## Ограничения

- Сборки v1 и v2 не синхронизируются автоматически: скиллы и шаблоны — копии, персону при правках нужно менять в обеих.
- Чтение `COURSE.md` — действие модели по инструкции из персоны, а не механизм OpenCode.
- Проверка актуальности программы зависит от доступа агента к веб-поиску: нет доступа — агент честно скажет и предложит источники для самостоятельной проверки.
- Если в глобальном `~/.config/opencode/opencode.json` уже задан другой `default_agent`, проектный конфиг его перекроет — это ожидаемо.

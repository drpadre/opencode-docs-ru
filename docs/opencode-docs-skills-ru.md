# Навыки агентов (Agent Skills)

Определите повторно используемое поведение с помощью определений `SKILL.md`.

## Размещение файлов (Place files)

Создайте папку с именем навыка и поместите внутрь `SKILL.md`. OpenCode ищет в:
*   `.opencode/skill/<name>/SKILL.md` (в проекте)
*   `~/.config/opencode/skill/<name>/SKILL.md` (глобально)
*   `.claude/skills/...` (совместимость с Claude)

## Frontmatter

Каждый `SKILL.md` должен начинаться с YAML frontmatter:
*   `name` (обязательно): 1-64 символа, a-z0-9, дефисы. Должно совпадать с именем директории.
*   `description` (обязательно): 1-1024 символов. Краткое описание.

## Пример использования (Use an example)

`.opencode/skill/git-release/SKILL.md`:

```markdown
---
name: git-release
description: Create consistent releases and changelogs
license: MIT
---

## What I do
- Draft release notes from merged PRs
- Propose a version bump

## When to use me
Use this when you are preparing a tagged release.
```

## Как это работает

Агент видит доступные навыки в описании инструмента `skill`. Он загружает навык, вызывая `skill({ name: "git-release" })`.

## Настройка разрешений (Configure permissions)

В `opencode.json`:

```json
{
  "permission": {
    "skill": {
      "pr-review": "allow",
      "internal-*": "deny",
      "*" : "allow"
    }
  }
}
```

## Отключение инструмента skill

Вы можете полностью отключить навыки для агента:

```json
{
  "agent": {
    "plan": {
      "tools": { "skill": false }
    }
  }
}
```

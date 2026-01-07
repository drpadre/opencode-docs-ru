# Команды (Commands)
Создавайте пользовательские команды для повторяющихся задач.

## Создание файлов команд (Create command files)

Создайте Markdown файлы в директории `command/` (глобально в `~/.config/opencode/command/` или в проекте в `.opencode/command/`).

Пример `.opencode/command/test.md`:

```markdown
---
description: Run tests with coverage
agent: build
model: anthropic/claude-3-5-sonnet-20241022
---
Run the full test suite with coverage report and show any failures.
Focus on the failing tests and suggest fixes.
```

Используйте команду, набрав `/test`.

## Настройка (Configure)

Вы также можете добавлять команды через `opencode.json`.

```json
{
  "command": {
    "test": {
      "template": "Run the full test suite...",
      "description": "Run tests with coverage",
      "agent": "build"
    }
  }
}
```

## Конфигурация промпта (Prompt config)

### Аргументы (Arguments)
Используйте `$ARGUMENTS` для подстановки всех аргументов или `$1`, `$2` для позиционных.

```markdown
Run tests for $1
```
Вызов: `/test auth` -> "Run tests for auth".

### Вывод оболочки (Shell output)
Используйте `!command`, чтобы внедрить вывод bash-команды.

```markdown
Here are the current test results:
!`npm test`
Based on these results...
```

### Ссылки на файлы (File references)
Используйте `@filename` для включения содержимого файла.

```markdown
Review the component in @src/components/Button.tsx.
```

## Опции (Options)

*   `template`: Промпт, который будет отправлен LLM (обязательно).
*   `description`: Краткое описание для TUI.
*   `agent`: Агент для выполнения команды.
*   `subtask`: `true/false`. Заставить команду выполнить вызов субагента (не засорять основной контекст).
*   `model`: Переопределить модель.

## Встроенные команды (Built-in)

OpenCode включает встроенные команды, такие как `/init`, `/undo`, `/redo`, `/share`, `/help`. Пользовательские команды с тем же именем переопределяют встроенные.

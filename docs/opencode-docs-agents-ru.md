# Агенты (Agents)

Настройка и использование специализированных агентов.

## Типы (Types)

В OpenCode есть два типа агентов: основные агенты (primary agents) и субагенты (subagents).

### Основные агенты (Primary agents)
Основные агенты — это главные помощники, с которыми вы взаимодействуете напрямую. Вы можете переключаться между ними, используя клавишу `Tab` или настроенную привязку `switch_agent`.

OpenCode поставляется с двумя встроенными основными агентами: **Build** и **Plan**.

### Субагенты (Subagents)
Субагенты — это специализированные помощники, которых основные агенты могут вызывать для конкретных задач. Вы также можете вручную вызывать их, упоминая через `@` в ваших сообщениях.

OpenCode поставляется с двумя встроенными субагентами: **General** и **Explore**.

## Встроенные (Built-in)

### Build
**Mode**: `primary`
Агент по умолчанию со всеми включенными инструментами. Это стандартный агент для задач разработки.

### Plan
**Mode**: `primary`
Ограниченный агент, предназначенный для планирования и анализа. По умолчанию все инструменты редактирования и выполнения команд требуют подтверждения (`ask`).

### General
**Mode**: `subagent`
Агент общего назначения для исследования сложных вопросов и выполнения многошаговых задач.

### Explore
**Mode**: `subagent`
Быстрый агент, специализированный на исследовании кодовой базы.

## Использование (Usage)

1.  Для основных агентов используйте `Tab` для переключения во время сессии.
2.  Субагенты могут быть вызваны:
    *   Автоматически основными агентами.
    *   Вручную через упоминание `@subagentName`.
3.  Навигация между сессиями (родительская <-> субагент): `<Leader>+Right` / `<Leader>+Left`.

## Настройка (Configure)

Вы можете настраивать агентов через JSON конфиг или Markdown файлы.

### JSON
В `opencode.json`:

```json
{
  "agent": {
    "code-reviewer": {
      "description": "Reviews code for best practices",
      "mode": "subagent",
      "model": "anthropic/claude-sonnet-4-20250514",
      "tools": { "write": false, "edit": false }
    }
  }
}
```

### Markdown
В `~/.config/opencode/agent/` или `.opencode/agent/`:

```markdown
---
description: Reviews code for quality
mode: subagent
tools:
  write: false
  edit: false
---

You are in code review mode. Focus on code quality and best practices.
```

Имя файла становится именем агента (например, `review.md` -> `review`).

## Опции (Options)

*   `description`: Краткое описание того, что делает агент (обязательно).
*   `temperature`: Управляет креативностью (0.0 - 1.0).
*   `maxSteps`: Максимальное количество шагов перед принудительным текстовым ответом.
*   `disable`: Отключить агента.
*   `prompt`: Путь к файлу с системным промптом (для JSON конфига).
*   `model`: Переопределить модель для агента.
*   `tools`: Включить/отключить инструменты.
*   `permissions`: Настроить разрешения для инструментов (`allow`, `ask`, `deny`).
*   `mode`: `primary`, `subagent`, или `all`.

### Дополнительные опции
Любые другие опции передаются напрямую провайдеру (например, `reasoningEffort` для OpenAI o1/o3).

## Создание агентов (Create agents)

Команда для интерактивного создания агента:

```bash
opencode agent create
```

## Примеры (Examples)

### Documentation agent
```markdown
---
description: Writes and maintains project documentation
mode: subagent
tools:
  bash: false
---
You are a technical writer. Create clear, comprehensive documentation.
```

### Security auditor
```markdown
---
description: Performs security audits
mode: subagent
tools:
  write: false
  edit: false
---
You are a security expert. Focus on identifying potential security issues.
```

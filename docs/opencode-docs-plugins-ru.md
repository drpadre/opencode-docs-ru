# Плагины (Plugins)

Пишите свои собственные плагины для расширения OpenCode.

## Использование плагина (Use a plugin)

### Из локальных файлов
Поместите JS/TS файлы в:
*   `.opencode/plugin/` (в проекте)
*   `~/.config/opencode/plugin/` (глобально)

### Из npm
Укажите в конфиге:
```json
{
  "plugin": ["opencode-wakatime", "@my-org/custom-plugin"]
}
```

## Создание плагина (Create a plugin)

Плагин — это функция, которая возвращает объект с хуками.

```javascript
export const MyPlugin = async ({ project, client, $, directory }) => {
  console.log("Plugin initialized!")
  return {
    // Хуки
  }
}
```

### Примеры хуков

#### Отправка уведомений
```javascript
return {
  event: async ({ event }) => {
    if (event.type === "session.idle") {
      await $`osascript -e 'display notification "Done!"'`
    }
  }
}
```

#### Защита .env файлов
```javascript
return {
  "tool.execute.before": async (input, output) => {
    if (input.tool === "read" && output.args.filePath.includes(".env")) {
      throw new Error("Do not read .env files")
    }
  }
}
```

#### Пользовательские инструменты
```javascript
import { tool } from "@opencode-ai/plugin"
return {
  tool: {
    mytool: tool({ ... })
  }
}
```

### События (Events)
Плагины могут подписываться на множество событий:
*   `session.created`, `session.updated`, `session.error`
*   `file.edited`
*   `command.executed`
*   `tool.execute.before`, `tool.execute.after`
*   и другие.

# Поддержка ACP (ACP Support)

Используйте OpenCode в любом редакторе, совместимом с ACP (Agent Control Protocol).

## Настройка (Configure)

Чтобы использовать OpenCode через ACP, настройте ваш редактор на запуск команды:

```bash
opencode acp
```

### Zed

Добавьте в `~/.config/zed/settings.json`:

```json
{
  "agent_servers": {
    "OpenCode": {
      "command": "opencode",
      "args": ["acp"]
    }
  }
}
```

### JetBrains IDEs

Добавьте в `acp.json`:

```json
{
  "agent_servers": {
    "OpenCode": {
      "command": "/absolute/path/bin/opencode",
      "args": ["acp"]
    }
  }
}
```

### Avante.nvim

```lua
{ acp_providers = { ["opencode"] = { command = "opencode", args = { "acp" } } } }
```

### CodeCompanion.nvim

```lua
require("codecompanion").setup({
  strategies = {
    chat = {
      adapter = { name = "opencode", model = "claude-sonnet-4" },
    },
  },
})
```

## Поддержка (Support)

OpenCode работает через ACP так же, как и в терминале. Поддерживаются все функции, включая инструменты, MCP сервера и агенты.
Примечание: Некоторые встроенные слэш-команды (например, `/undo`, `/redo`) в настоящее время не поддерживаются.

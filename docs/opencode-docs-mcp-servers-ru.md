# MCP сервера (MCP Servers)

Добавляйте локальные и удаленные инструменты MCP (Model Context Protocol).

## Включение (Enable)

Определите MCP сервера в вашем конфиге OpenCode в разделе `mcp`.

```json
{
  "mcp": {
    "name-of-mcp-server": {
      "type": "local",
      "command": ["npx", "-y", "my-mcp-command"],
      "enabled": true
    }
  }
}
```

## Локальные (Local)

Добавляйте локальные MCP сервера, используя `"type": "local"`.

```json
{
  "mcp": {
    "mcp_everything": {
      "type": "local",
      "command": ["npx", "-y", "@modelcontextprotocol/server-everything"]
    }
  }
}
```

## Удаленные (Remote)

Добавляйте удаленные MCP сервера, используя `"type": "remote"`.

```json
{
  "mcp": {
    "my-remote-mcp": {
      "type": "remote",
      "url": "https://my-mcp-server.com",
      "headers": { "Authorization": "Bearer MY_API_KEY" }
    }
  }
}
```

## OAuth

OpenCode автоматически обрабатывает OAuth аутентификацию для удаленных MCP серверов (детектирует 401, инициирует поток, сохраняет токены).

### Аутентификация
Вручную:
```bash
opencode mcp auth my-oauth-server
```
Список:
```bash
opencode mcp list
```

## Управление (Manage)

Ваши MCP инструменты доступны в OpenCode наравне со встроенными.

### Глобально (Global)
Можно отключить инструменты глобально в `tools`.

```json
{
  "tools": { "my-mcp*": false }
}
```

### Для агента (Per agent)
Можно включить только для конкретного агента.

## Примеры (Examples)

### Sentry
```json
{ "mcp": { "sentry": { "type": "remote", "url": "https://mcp.sentry.dev/mcp" } } }
```

### Context7
Поиск по документации.
```json
{ "mcp": { "context7": { "type": "remote", "url": "https://mcp.context7.com/mcp" } } }
```

### Grep by Vercel
Поиск по коду на GitHub.
```json
{ "mcp": { "gh_grep": { "type": "remote", "url": "https://mcp.grep.app" } } }
```

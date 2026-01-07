# SDK

Типобезопасный JS клиент для сервера OpenCode.

## Установка (Install)

```bash
npm install @opencode-ai/sdk
```

## Создание клиента (Create client)

```javascript
import { createOpencode } from "@opencode-ai/sdk"
const { client } = await createOpencode()
```
Это запускает сервер и создает к нему клиент.

Если у вас уже есть запущенный экземпляр:
```javascript
import { createOpencodeClient } from "@opencode-ai/sdk"
const client = createOpencodeClient({
  baseUrl: "http://localhost:4096",
})
```

## API (APIs)

SDK предоставляет доступ ко всем API сервера.

### Global
```javascript
const health = await client.global.health()
```

### App
```javascript
await client.app.log({ body: { service: "my-app", level: "info", message: "Done" } })
const agents = await client.app.agents()
```

### Project
```javascript
const projects = await client.project.list()
```

### Session
```javascript
// Создать сессию
const session = await client.session.create({ body: { title: "My session" } })

// Отправить промпт
const result = await client.session.prompt({
  path: { id: session.id },
  body: {
    model: { providerID: "anthropic", modelID: "claude-3-5-sonnet-20241022" },
    parts: [{ type: "text", text: "Hello!" }],
  },
})
```

### Files
```javascript
// Поиск файлов
const files = await client.find.files({ query: { query: "*.ts", type: "file" } })
// Чтение файла
const content = await client.file.read({ query: { path: "src/index.ts" } })
```

### TUI
Управление интерфейсом TUI.
```javascript
await client.tui.showToast({ body: { message: "Task completed", variant: "success" } })
```

### Events
Подписка на события в реальном времени.
```javascript
const events = await client.event.subscribe()
for await (const event of events.stream) {
  console.log("Event:", event.type, event.properties)
}
```

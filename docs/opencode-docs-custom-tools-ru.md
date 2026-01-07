# Пользовательские инструменты (Custom Tools)

Создавайте инструменты, которые LLM может вызывать в OpenCode.

## Создание инструмента (Creating a tool)

Инструменты определяются как файлы JavaScript или TypeScript.
Они могут располагаться:
*   В проекте: `.opencode/tool/`
*   Глобально: `~/.config/opencode/tool/`

### Структура (Structure)

Используйте хелпер `tool()` для типобезопасности.

```javascript
import { tool } from "@opencode-ai/plugin"

export default tool({
  description: "Query the project database",
  args: {
    query: tool.schema.string().describe("SQL query to execute"),
  },
  async execute(args) {
    // Ваша логика
    return `Executed query: ${args.query}`
  },
})
```
Имя файла становится именем инструмента (например, `database.ts` -> `database`).

### Несколько инструментов в одном файле

```javascript
export const add = tool({ ... })
export const multiply = tool({ ... })
```
Создает инструменты `filename_add` и `filename_multiply`.

### Аргументы (Arguments)

Используется [Zod](https://zod.dev) для определения типов аргументов.

### Контекст (Context)

Инструменты получают контекст о текущей сессии:

```javascript
async execute(args, context) {
  const { agent, sessionID, messageID } = context
  // ...
}
```

## Примеры (Examples)

### Написание инструмента на Python

Можно написать инструмент на любом языке и вызвать его из JS определения.

`add.py`:
```python
import sys
print(int(sys.argv[1]) + int(sys.argv[2]))
```

Инструмент `add.ts`:
```javascript
import { tool } from "@opencode-ai/plugin"
export default tool({
  description: "Add two numbers using Python",
  args: {
    a: tool.schema.number(),
    b: tool.schema.number(),
  },
  async execute(args) {
    // Используем bun shell или child_process для вызова скрипта
    const result = await Bun.$`python3 .opencode/tool/add.py ${args.a} ${args.b}`.text()
    return result.trim()
  },
})
```

# Форматтеры (Formatters)

OpenCode использует специфичные для языка форматтеры.

## Встроенные (Built-in)

OpenCode поставляется с несколькими встроенными форматтерами:
*   `prettier` (JS, TS, JSON, CSS, etc.)
*   `gofmt` (Go)
*   `mix` (Elixir)
*   `shfmt` (Shell)
*   `rustfmt` (Rust)
*   `ruff` (Python)
*   и многие другие.

Если в вашем проекте есть `prettier` в `package.json`, OpenCode будет использовать его автоматически.

## Как это работает (How it works)
Когда OpenCode пишет или редактирует файл, он:
1.  Проверяет расширение файла.
2.  Запускает соответствующий форматтер.
3.  Автоматически применяет изменения форматирования.

## Настройка (Configure)

Вы можете настроить форматтеры в `opencode.json`.

### Отключение форматтеров

Глобально:
```json
{ "formatter": false }
```

Конкретный форматтер:
```json
{
  "formatter": {
    "prettier": { "disabled": true }
  }
}
```

### Пользовательские форматтеры (Custom formatters)

Переопределение или добавление новых:

```json
{
  "formatter": {
    "custom-markdown": {
      "command": ["deno", "fmt", "$FILE"],
      "extensions": [".md"]
    }
  }
}
```
`$FILE` заменяется на путь к файлу.

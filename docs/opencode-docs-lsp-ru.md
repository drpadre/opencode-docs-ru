# LSP сервера (LSP Servers)

OpenCode интегрируется с вашими LSP серверами.

## Встроенные (Built-in)

OpenCode поставляется с несколькими встроенными LSP серверами для популярных языков (typescript, go, rust-analyzer, python, ruby, java, csharp и др.).
Они включаются автоматически при обнаружении соответствующих расширений файлов.

Вы можете отключить автоматическую загрузку, установив переменную окружения `OPENCODE_DISABLE_LSP_DOWNLOAD=true`.

## Настройка (Configure)

Вы можете настроить LSP в `opencode.json`.

### Отключение

Глобально:
```json
{ "lsp": false }
```

Конкретный сервер:
```json
{
  "lsp": {
    "typescript": { "disabled": true }
  }
}
```

### Пользовательские LSP сервера (Custom LSP servers)

```json
{
  "lsp": {
    "custom-lsp": {
      "command": ["custom-lsp-server", "--stdio"],
      "extensions": [".custom"]
    }
  }
}
```

## Дополнительная информация

### PHP Intelephense
PHP Intelephense требует лицензионный ключ для премиум-функций. Поместите ключ в файл `licence.txt` в:
*   macOS/Linux: `$HOME/intelephense/licence.txt`
*   Windows: `%USERPROFILE%/intelephense/licence.txt`

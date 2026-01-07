# Горячие клавиши (Keybinds)

Настройте свои горячие клавиши.

В OpenCode есть набор действий по умолчанию, которые можно переопределить в файле `opencode.json`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {
    "leader": "ctrl+x",
    "session_new": "<leader>n",
    "session_list": "<leader>l",
    "input_submit": "return",
    "input_newline": "shift+return,ctrl+return"
  }
}
```

## Клавиша-лидер (Leader key)

OpenCode использует клавишу-лидер для большинства комбинаций, чтобы избежать конфликтов в терминале. По умолчанию это `ctrl+x`.

## Отключение горячих клавиш (Disable keybind)

Вы можете отключить привязку, установив значение `"none"`.

```json
{ "keybinds": { "session_compact": "none" } }
```

## Горячие клавиши ввода (Desktop prompt shortcuts)

Приложение OpenCode поддерживает стандартные клавиатурные сокращения в стиле Readline/Emacs для редактирования текста (например, `ctrl+a`, `ctrl+e`, `ctrl+k`).

## Shift+Enter

Некоторые терминалы по умолчанию не отправляют модификаторы с Enter.
Для Windows Terminal вам может потребоваться добавить действие `sendInput` с последовательностью `\u001b[13;2u` для `shift+enter` в `settings.json`.

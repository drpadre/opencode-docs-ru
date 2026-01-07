# IDE (Интегрированная среда разработки)

Расширение OpenCode для VS Code, Cursor и других IDE.

## Использование (Usage)

-   **Быстрый запуск (Quick Launch)**: Используйте `Cmd+Esc` (Mac) или `Ctrl+Esc` (Windows/Linux), чтобы открыть OpenCode в разделенном терминале, или сфокусироваться на существующей сессии терминала, если она уже запущена.
-   **Новая сессия (New Session)**: Используйте `Cmd+Shift+Esc` (Mac) или `Ctrl+Shift+Esc` (Windows/Linux), чтобы начать новую сессию терминала OpenCode, даже если она уже открыта. Вы также можете нажать кнопку OpenCode в интерфейсе.
-   **Осведомленность о контексте (Context Awareness)**: Автоматически делится вашим текущим выделением или вкладкой с OpenCode.
-   **Горячие клавиши для ссылок на файлы**: Используйте `Cmd+Option+K` (Mac) или `Alt+Ctrl+K` (Linux/Windows), чтобы вставить ссылки на файлы. Например, `@File#L37-42`.

## Установка (Installation)

Чтобы установить OpenCode на VS Code и популярные форки, такие как Cursor, Windsurf, VSCodium:

1.  Откройте VS Code.
2.  Откройте интегрированный терминал.
3.  Запустите `opencode` - расширение установится автоматически.

```bash
opencode
```

Если вы хотите использовать свою собственную IDE, когда запускаете `/editor` или `/export` из TUI, вам нужно установить переменную окружения `EDITOR`. [Узнайте больше](opencode-docs-tui-ru.md#editor-setup).

```bash
export EDITOR="code --wait"
```

### Ручная установка (Manual Install)

Найдите **OpenCode** в Extension Marketplace и нажмите **Install**.

### Устранение неполадок (Troubleshooting)

Если расширение не удается установить автоматически:

-   Убедитесь, что вы запускаете `opencode` в интегрированном терминале.
-   Подтвердите, что CLI для вашей IDE установлен:
    *   Для VS Code: команда `code`
    *   Для Cursor: команда `cursor`
    *   Для Windsurf: команда `windsurf`
    *   Для VSCodium: команда `codium`
-   Если нет, запустите `Cmd+Shift+P` (Mac) или `Ctrl+Shift+P` (Windows/Linux) и найдите «Shell Command: Install ‘code’ command in PATH» (или эквивалент для вашей IDE).
-   Убедитесь, что у VS Code есть разрешение на установку расширений.

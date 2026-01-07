# Переход на 1.0 (Migrating to 1.0)

Что нового в OpenCode 1.0.

## Обновление (Upgrading)

Чтобы обновиться вручную, выполните:
```bash
$ opencode upgrade 1.0.0
```

Чтобы вернуться откатиться к 0.x, выполните:
```bash
$ opencode upgrade 0.15.31
```

## Изменения в UX (UX changes)

*   История сессии более сжата.
*   Добавлена командная панель (Command bar): `ctrl+p`.
*   Добавлена боковая панель сессии (Session sidebar).

## Критические изменения (Breaking changes)

### Переименованные горячие клавиши
*   `messages_revert` -> `messages_undo`
*   `switch_agent` -> `agent_cycle`
*   `switch_agent_reverse` -> `agent_cycle_reverse`
*   `switch_mode` -> `agent_cycle`
*   `switch_mode_reverse` -> `agent_cycle_reverse`

### Удаленные горячие клавиши
*   `messages_layout_toggle`
*   `messages_next` (и `previous`)
*   `file_diff_toggle`
*   `file_search`
*   `file_close`
*   `file_list`
*   `app_help`
*   `project_init`
*   `tool_details`
*   `thinking_blocks`

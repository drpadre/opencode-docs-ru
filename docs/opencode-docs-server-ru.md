# Сервер (Server)

Взаимодействуйте с сервером OpenCode через HTTP.

## Использование (Usage)

Запустите автономный сервер:
```bash
opencode serve [--port 4096] [--hostname 127.0.0.1]
```
Если у вас уже запущен OpenCode TUI, он также запускает сервер.

## Спецификация (Spec)
OpenAPI спецификация доступна по адресу:
`http://<hostname>:<port>/doc` (например, `http://localhost:4096/doc`).

## API

### Global
*   `GET /global/health`: Проверка работоспособности.

### Session
*   `GET /session`: Список сессий.
*   `POST /session`: Создать сессию.
*   `GET /session/:id`: Получить сессию.
*   `POST /session/:id/prompt`: Отправить сообщение.

### Files
*   `GET /find?pattern=<pat>`: Поиск текста.
*   `GET /find/file?query=<q>`: Поиск файлов.
*   `GET /file/content?path=<p>`: Чтение содержимого файла.

### TUI
Эндпоинты для управления TUI (открытие справки, управление промптом, показ уведомлений).

Более подробую информацию см. в сгенерированных [SDK типах](https://github.com/anomalyco/opencode/blob/dev/packages/sdk/js/src/gen/types.gen.ts).

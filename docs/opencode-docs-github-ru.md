# GitHub

Используйте OpenCode в GitHub issues и pull-requests.

## Возможности (Features)

*   **Triage issues**: Попросите OpenCode изучить проблему и объяснить её вам.
*   **Fix and implement**: Попросите OpenCode исправить проблему или реализовать функцию. Он будет работать в новой ветке и отправит PR со всеми изменениями.
*   **Secure**: OpenCode работает внутри ваших GitHub runners.

## Установка (Installation)

Запустите следующую команду в проекте, который находится в репозитории GitHub:

```bash
opencode github install
```

Это проведет вас через установку приложения GitHub, создание рабочего процесса (workflow) и настройку секретов.

### Ручная настройка (Manual Setup)

1.  **Установите GitHub app**
    Перейдите на [github.com/apps/opencode-agent](https://github.com/apps/opencode-agent). Убедитесь, что оно установлено в целевом репозитории.

2.  **Добавьте рабочий процесс (workflow)**
    Добавьте следующий файл рабочего процесса в `.github/workflows/opencode.yml` в вашем репозитории. Обязательно установите соответствующую модель и необходимые API ключи в `env`.

    ```yaml
    name: opencode
    on:
      issue_comment:
        types: [created]
      pull_request_review_comment:
        types: [created]
    jobs:
      opencode:
        if: |
          contains(github.event.comment.body, '/oc') ||
          contains(github.event.comment.body, '/opencode')
        runs-on: ubuntu-latest
        permissions:
          id-token: write
        steps:
          - name: Checkout repository
            uses: actions/checkout@v6
            with:
              fetch-depth: 1
          - name: Run OpenCode
            uses: anomalyco/opencode/github@latest
            env:
              ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
            with:
              model: anthropic/claude-sonnet-4-20250514
              # share: true
              # github_token: xxxx
    ```

3.  **Сохраните API ключи в секретах**
    В настройках вашей организации или проекта, разверните Secrets and variables слева и выберите Actions. И добавьте необходимые API ключи.

## Конфигурация (Configuration)

*   `model`: Модель для использования с OpenCode. Формат: `provider/model`. (Обязательно)
*   `agent`: Агент для использования.
*   `share`: Будет ли сессия OpenCode расшарена. По умолчанию `true` для публичных репозиториев.
*   `prompt`: Опциональный пользовательский промпт для переопределения поведения по умолчанию.
*   `token`: Опциональный токен доступа GitHub.

## Поддерживаемые события (Supported Events)

OpenCode может быть запущен следующими событиями GitHub:
*   `issue_comment` (при наличии `/opencode` или `/oc`)
*   `pull_request_review_comment` (при наличии `/opencode` или `/oc`)
*   `issues` (требуется `prompt`)
*   `pull_request` (требуется `prompt`)
*   `schedule` (требуется `prompt`)
*   `workflow_dispatch` (требуется `prompt`)

### Пример расписания (Schedule Example)

Запуск OpenCode по расписанию для выполнения автоматических задач:

```yaml
on:
  schedule:
    - cron: "0 9 * * 1" # Каждый понедельник в 9 утра UTC
# ...
with:
  prompt: |
    Review the codebase for any TODO comments and create a summary.
    If you find issues worth addressing, open an issue to track them.
```

### Пример Pull Request

Автоматический обзор PR при их открытии или обновлении:

```yaml
on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]
# ...
with:
  prompt: |
    Review this pull request:
    - Check for code quality issues
    - Look for potential bugs
    - Suggest improvements
```

### Пример сортировки задач (Issues Triage)

Автоматическая сортировка (triage) новых задач. Можно использовать фильтры (например, возраст аккаунта) перед запуском OpenCode.

## Примеры (Examples)

*   **Объяснить проблему**: В GitHub issue напишите `/opencode explain this issue`.
*   **Исправить проблему**: В GitHub issue напишите `/opencode fix this`.
*   **Обзор PR и внесение изменений**: Оставьте комментарий в GitHub PR: `Delete the attachment from S3 when the note is removed /oc`.
*   **Обзор конкретных строк кода**: Оставьте комментарий прямо к строкам кода во вкладке "Files" PR: `/oc add error handling here`.

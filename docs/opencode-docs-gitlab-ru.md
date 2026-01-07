# GitLab

Используйте OpenCode в GitLab issues и merge requests.

## GitLab CI

OpenCode работает в обычном пайплайне GitLab. Вы можете встроить его в пайплайн как [CI компонент](https://docs.gitlab.com/ee/ci/components/).
Здесь мы используем созданный сообществом CI/CD компонент для OpenCode — [nagyv/gitlab-opencode](https://gitlab.com/nagyv/gitlab-opencode).

### Возможности (Features)

*   **Используйте пользовательскую конфигурацию для каждой задачи**: Настройте OpenCode с пользовательским каталогом конфигурации, например `./config/#custom-directory`, чтобы включить или отключить функциональность для каждого вызова OpenCode.
*   **Минимальная настройка**: CI компонент настраивает OpenCode в фоновом режиме, вам нужно только создать конфигурацию OpenCode и начальный промпт.
*   **Гибкость**: CI компонент поддерживает несколько вводных параметров для настройки его поведения.

### Настройка (Setup)

1.  Сохраните ваш JSON аутентификации OpenCode как переменную окружения CI типа **File** в Settings > CI/CD > Variables. Обязательно пометьте их как "Masked and hidden".
2.  Добавьте следующее в ваш файл `.gitlab-ci.yml`.

```yaml
include:
  - component: $CI_SERVER_FQDN/nagyv/gitlab-opencode/opencode@2
    inputs:
      config_dir: ${CI_PROJECT_DIR}/opencode-config
      auth_json: $OPENCODE_AUTH_JSON # Имя переменной для вашего JSON аутентификации OpenCode
      command: optional-custom-command
      message: "Your prompt here"
```

## GitLab Duo

OpenCode интегрируется с вашим рабочим процессом GitLab. Упомяните `@opencode` в комментарии, и OpenCode выполнит задачи в вашем пайплайне GitLab CI.

### Возможности (Features)

*   **Triage issues**: Попросите OpenCode изучить проблему и объяснить её вам.
*   **Fix and implement**: Попросите OpenCode исправить проблему или реализовать функцию. Он создаст новую ветку и поднимет merge request с изменениями.
*   **Secure**: OpenCode работает на ваших GitLab runners.

### Настройка (Setup)

OpenCode работает в вашем пайплайне GitLab CI/CD.
Совет: Ознакомьтесь с [документацией GitLab](https://docs.gitlab.com/user/duo_agent_platform/agent_assistant/) для получения актуальных инструкций.

Пример конфигурации потока:

```yaml
image: node:22-slim
commands:
  - echo "Installing opencode"
  - npm install --global opencode-ai
  - echo "Installing glab"
  # ... (установка зависимостей и настройка) ...
  - |
    opencode run "
    You are an AI assistant helping with GitLab operations.
    Context: $AI_FLOW_CONTEXT
    Task: $AI_FLOW_INPUT
    Event: $AI_FLOW_EVENT
    Please execute the requested task using the available GitLab tools.
    Be thorough in your analysis and provide clear explanations.
    <important>
    Please use the glab CLI to access data from GitLab. The glab CLI has already been authenticated.
    If you are asked to summarize an MR or issue or asked to provide more information then please post back a note to the MR/Issue.
    You don't need to commit or push up changes, those will be done automatically based on the file changes you make.
    </important>
    "
  # ... (git commit & push) ...
variables:
  - ANTHROPIC_API_KEY
  - GITLAB_TOKEN_OPENCODE
  - GITLAB_HOST
```

### Примеры (Examples)

*   **Объяснить проблему**: В GitLab issue напишите `@opencode explain this issue`.
*   **Исправить проблему**: В GitLab issue напишите `@opencode fix this`.
*   **Обзор merge request**: Оставьте комментарий в GitLab MR: `@opencode review this merge request`.

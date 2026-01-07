# Конфигурация

Использование JSON-конфигурации OpenCode.

Вы можете настроить OpenCode, используя файл конфигурации JSON.

## Формат

OpenCode поддерживает форматы JSON и JSONC (JSON с комментариями).

```json
{
  "$schema": "https://opencode.ai/config.json", 
  // Конфигурация темы
  "theme": "opencode",
  "model": "anthropic/claude-sonnet-4-5",
  "autoupdate": true
}
```

## Расположение

Вы можете разместить свой конфиг в нескольких местах, и у них разный приоритет.

> **Примечание**: Файлы конфигурации объединяются, а не заменяются. Настройки из следующих мест расположения комбинируются. Более поздние конфиги переопределяют более ранние только в случае конфликта ключей. Неконфликтующие настройки из всех конфигов сохраняются.

Например, если ваш глобальный конфиг устанавливает `theme: "opencode"` и `autoupdate: true`, а ваш конфиг проекта устанавливает `model: "anthropic/claude-sonnet-4-5"`, итоговая конфигурация будет включать все три настройки.

### Глобальный

Разместите свой глобальный конфиг OpenCode в `~/.config/opencode/opencode.json`. Вы захотите использовать глобальный конфиг для таких вещей, как темы, провайдеры или горячие клавиши.

```bash
~/.config/opencode/opencode.json
```

### Для проекта

Вы также можете добавить `opencode.json` в свой проект. Настройки из этого конфига объединяются с глобальным конфигом и могут переопределять его. Это полезно для настройки провайдеров или режимов, специфичных для вашего проекта.

```bash
opencode.json
```

> **Совет**: Размещайте специфичный для проекта конфиг в корне вашего проекта.
Когда OpenCode запускается, он ищет файл конфигурации в текущей директории или переходит вверх до ближайшей директории Git.
Это также безопасно для добавления в Git, и используется та же схема, что и в глобальном.

### Пользовательский путь

Вы также можете указать пользовательский путь к файлу конфигурации, используя переменную окружения `OPENCODE_CONFIG`.

```bash
export OPENCODE_CONFIG=/path/to/my/custom-config.json
opencode run "Hello world"
```

Настройки из этого конфига объединяются с глобальным и проектным конфигами и могут переопределять их.

### Пользовательская директория

Вы можете указать пользовательскую директорию конфигурации, используя переменную окружения `OPENCODE_CONFIG_DIR`. В этой директории будет производиться поиск агентов, команд, режимов и плагинов точно так же, как в стандартной директории `.opencode`, и она должна следовать той же структуре.

```bash
export OPENCODE_CONFIG_DIR=/path/to/my/config-directory
opencode run "Hello world"
```

Пользовательская директория загружается после глобального конфига и директорий `.opencode`, поэтому она может переопределять их настройки.

## Схема

Файл конфигурации имеет схему, которая определена в [opencode.ai/config.json](https://opencode.ai/config.json).

Ваш редактор должен уметь валидировать и автодополнять на основе этой схемы.

### TUI

Вы можете настроить параметры, специфичные для TUI, через опцию `tui`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tui": {
    "scroll_speed": 3,
    "scroll_acceleration": {
      "enabled": true
    },
    "diff_style": "auto"
  }
}
```

Доступные опции:
*   `scroll_acceleration.enabled` - Включить ускорение прокрутки в стиле macOS. Имеет приоритет над `scroll_speed`.
*   `scroll_speed` - Пользовательский множитель скорости прокрутки (по умолчанию: 1, минимум: 1). Игнорируется, если `scroll_acceleration.enabled` установлено в true.
*   `diff_style` - Управление отображением diff. "auto" адаптируется к ширине терминала, "stacked" всегда показывает одну колонку.

[Узнайте больше об использовании TUI здесь](opencode-docs-tui-ru.md).

### Server

Вы можете настроить параметры сервера для команд `opencode serve` и `opencode web` через опцию `server`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "server": {
    "port": 4096,
    "hostname": "0.0.0.0",
    "mdns": true,
    "cors": ["http://localhost:5173"]
  }
}
```

Доступные опции:
*   `port` - Порт для прослушивания.
*   `hostname` - Хостнейм для прослушивания. Когда включен `mdns` и `hostname` не задан, по умолчанию используется `0.0.0.0`.
*   `mdns` - Включить обнаружение сервисов mDNS. Это позволяет другим устройствам в сети обнаруживать ваш сервер OpenCode.
*   `cors` - Дополнительные источники (origins), разрешенные для CORS при использовании HTTP-сервера из браузерного клиента. Значения должны быть полными origins (схема + хост + опциональный порт), например `https://app.example.com`.

[Узнайте больше о сервере здесь](opencode-docs-server-ru.md).

### Tools

Вы можете управлять инструментами, которые может использовать LLM, через опцию `tools`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tools": {
    "write": false,
    "bash": false
  }
}
```

[Узнайте больше об инструментах здесь](opencode-docs-tools-ru.md).

### Models

Вы можете настроить провайдеров и модели, которые хотите использовать в своем конфиге OpenCode, через опции `provider`, `model` и `small_model`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {},
  "model": "anthropic/claude-sonnet-4-5",
  "small_model": "anthropic/claude-haiku-4-5"
}
```

Опция `small_model` настраивает отдельную модель для легковесных задач, таких как генерация заголовков. По умолчанию OpenCode пытается использовать более дешевую модель, если она доступна у вашего провайдера, в противном случае он переключается на вашу основную модель.

Опции провайдера могут включать `timeout` и `setCacheKey`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": {
        "timeout": 600000,
        "setCacheKey": true
      }
    }
  }
}
```

*   `timeout` - Таймаут запроса в миллисекундах (по умолчанию: 300000). Установите `false`, чтобы отключить.
*   `setCacheKey` - Обеспечить, чтобы ключ кэша всегда устанавливался для указанного провайдера.

Вы также можете настроить [локальные модели](opencode-docs-models-ru.md#local). [Узнать больше](opencode-docs-models-ru.md).

#### Специфичные опции провайдеров

Некоторые провайдеры поддерживают дополнительные опции конфигурации помимо общих `timeout` и `apiKey`.

##### Amazon Bedrock

Amazon Bedrock поддерживает конфигурацию, специфичную для AWS:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "amazon-bedrock": {
      "options": {
        "region": "us-east-1",
        "profile": "my-aws-profile",
        "endpoint": "https://bedrock-runtime.us-east-1.vpce-xxxxx.amazonaws.com"
      }
    }
  }
}
```

*   `region` - Регион AWS для Bedrock (по умолчанию берется из переменной окружения `AWS_REGION` или `us-east-1`)
*   `profile` - Именованный профиль AWS из `~/.aws/credentials` (по умолчанию берется из переменной окружения `AWS_PROFILE`)
*   `endpoint` - Пользовательский URL эндпоинта для VPC эндпоинтов. Это псевдоним для общей опции `baseURL`, использующий терминологию AWS. Если указаны оба, `endpoint` имеет приоритет.

> **Примечание**: Bearer токены (`AWS_BEARER_TOKEN_BEDROCK` или `/connect`) имеют приоритет над аутентификацией по профилю. См. [приоритет аутентификации](opencode-docs-providers-ru.md#authentication-precedence) для подробностей.

[Узнайте больше о конфигурации Amazon Bedrock](opencode-docs-providers-ru.md#amazon-bedrock).

### Themes

Вы можете настроить, какую тему использовать, через опцию `theme`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "theme": ""
}
```

[Узнайте больше здесь](opencode-docs-themes-ru.md).

### Agents

Вы можете настроить специализированных агентов для конкретных задач через опцию `agent`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "code-reviewer": {
      "description": "Reviews code for best practices and potential issues",
      "model": "anthropic/claude-sonnet-4-5",
      "prompt": "You are a code reviewer. Focus on security, performance, and maintainability.",
      "tools": {
        // Отключить инструменты модификации файлов для агента, занимающегося только проверкой
        "write": false,
        "edit": false
      }
    }
  }
}
```

Вы также можете определять агентов, используя markdown-файлы в `~/.config/opencode/agent/` или `.opencode/agent/`. [Узнайте больше здесь](opencode-docs-agents-ru.md).

### Default agent (Агент по умолчанию)

Вы можете установить агента по умолчанию, используя опцию `default_agent`. Это определяет, какой агент будет использоваться, если ни один не указан явно.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "plan"
}
```

Агент по умолчанию должен быть основным агентом (не субагентом). Это может быть встроенный агент, такой как "build" или "plan", или [пользовательский агент](opencode-docs-agents-ru.md), которого вы определили. Если указанный агент не существует или является субагентом, OpenCode вернется к "build" с предупреждением.

Эта настройка применяется ко всем интерфейсам: TUI, CLI (`opencode run`), десктопному приложению и GitHub Action.

### Sharing

Вы можете настроить функцию [шаринга](opencode-docs-share-ru.md) через опцию `share`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "share": "manual"
}
```

Принимает значения:
*   `"manual"` - Разрешить шаринг вручную через команды (по умолчанию)
*   `"auto"` - Автоматически шарить новые разговоры
*   `"disabled"` - Полностью отключить шаринг

По умолчанию шаринг установлен в ручной режим, когда вам нужно явно делиться разговорами, используя команду `/share`.

### Commands

Вы можете настроить пользовательские команды для повторяющихся задач через опцию `command`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "command": {
    "test": {
      "template": "Run the full test suite with coverage report and show any failures.\nFocus on the failing tests and suggest fixes.",
      "description": "Run tests with coverage",
      "agent": "build",
      "model": "anthropic/claude-haiku-4-5"
    },
    "component": {
      "template": "Create a new React component named $ARGUMENTS with TypeScript support.\nInclude proper typing and basic structure.",
      "description": "Create a new component"
    }
  }
}
```

Вы также можете определять команды, используя markdown-файлы в `~/.config/opencode/command/` или `.opencode/command/`. [Узнайте больше здесь](opencode-docs-commands-ru.md).

### Keybinds

Вы можете настроить свои горячие клавиши через опцию `keybinds`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {}
}
```

[Узнайте больше здесь](opencode-docs-keybinds-ru.md).

### Autoupdate

OpenCode автоматически загружает новые обновления при запуске. Вы можете отключить это с помощью опции `autoupdate`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "autoupdate": false
}
```

Если вы не хотите обновлений, но хотите получать уведомления о доступности новой версии, установите `autoupdate` в `"notify"`.

### Formatters

Вы можете настроить форматтеры кода через опцию `formatter`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "formatter": {
    "prettier": {
      "disabled": true
    },
    "custom-prettier": {
      "command": ["npx", "prettier", "--write", "$FILE"],
      "environment": {
        "NODE_ENV": "development"
      },
      "extensions": [".js", ".ts", ".jsx", ".tsx"]
    }
  }
}
```

[Узнайте больше о форматтерах здесь](opencode-docs-formatters-ru.md).

### Permissions (Разрешения)

По умолчанию `opencode` разрешает все операции без явного одобрения. Вы можете изменить это, используя опцию `permission`.

Например, чтобы гарантировать, что инструменты `edit` и `bash` требуют одобрения пользователя:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "ask",
    "bash": "ask"
  }
}
```

[Узнайте больше о разрешениях здесь](opencode-docs-permissions-ru.md).

### Compaction (Уплотнение)

Вы можете управлять поведением уплотнения контекста через опцию `compaction`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "compaction": {
    "auto": true,
    "prune": true
  }
}
```

*   `auto` - Автоматически уплотнять сессию, когда контекст заполнен (по умолчанию: true).
*   `prune` - Удалять старые выходные данные инструментов для экономии токенов (по умолчанию: true).

### Watcher

Вы можете настроить шаблоны игнорирования для отслеживания файлов через опцию `watcher`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "watcher": {
    "ignore": ["node_modules/**", "dist/**", ".git/**"]
  }
}
```

Шаблоны следуют синтаксису glob. Используйте это, чтобы исключить шумные директории из отслеживания файлов.

### MCP servers

Вы можете настроить MCP серверы, которые хотите использовать, через опцию `mcp`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {}
}
```

[Узнайте больше здесь](opencode-docs-mcp-servers-ru.md).

### Plugins

[Плагины](opencode-docs-plugins-ru.md) расширяют OpenCode пользовательскими инструментами, хуками и интеграциями.

Размещайте файлы плагинов в `.opencode/plugin/` или `~/.config/opencode/plugin/`. Вы также можете загружать плагины из npm через опцию `plugin`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-helicone-session", "@my-org/custom-plugin"]
}
```

[Узнайте больше здесь](opencode-docs-plugins-ru.md).

### Instructions (Инструкции)

Вы можете настроить инструкции для модели, которую используете, через опцию `instructions`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["CONTRIBUTING.md", "docs/guidelines.md", ".cursor/rules/*.md"]
}
```

Принимает массив путей и glob-шаблонов к файлам инструкций. [Узнайте больше о правилах здесь](opencode-docs-rules-ru.md).

### Disabled providers

Вы можете отключить провайдеров, которые загружаются автоматически, через опцию `disabled_providers`. Это полезно, когда вы хотите предотвратить загрузку определенных провайдеров, даже если их учетные данные доступны.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "disabled_providers": ["openai", "gemini"]
}
```

> **Примечание**: `disabled_providers` имеет приоритет над `enabled_providers`.

Опция `disabled_providers` принимает массив ID провайдеров. Когда провайдер отключен:
*   Он не будет загружен, даже если установлены переменные окружения.
*   Он не будет загружен, даже если API ключи настроены через команду `/connect`.
*   Модели провайдера не появятся в списке выбора моделей.

### Enabled providers

Вы можете указать список разрешенных провайдеров через опцию `enabled_providers`. Если установлено, только указанные провайдеры будут включены, а все остальные будут проигнорированы.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "enabled_providers": ["anthropic", "openai"]
}
```

Это полезно, когда вы хотите ограничить OpenCode использованием только конкретных провайдеров, вместо того чтобы отключать их по одному.

> **Примечание**: `disabled_providers` имеет приоритет над `enabled_providers`.

Если провайдер появляется и в `enabled_providers`, и в `disabled_providers`, `disabled_providers` имеет приоритет для обратной совместимости.

### Experimental

Ключ `experimental` содержит опции, находящиеся в активной разработке.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "experimental": {}
}
```

> **Осторожно**: Экспериментальные опции нестабильны. Они могут измениться или быть удалены без предупреждения.

## Переменные

Вы можете использовать подстановку переменных в ваших файлах конфигурации, чтобы ссылаться на переменные окружения и содержимое файлов.

### Переменные окружения (Env vars)

Используйте `{env:VARIABLE_NAME}` для подстановки переменных окружения:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "{env:OPENCODE_MODEL}",
  "provider": {
    "anthropic": {
      "models": {},
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}"
      }
    }
  }
}
```

Если переменная окружения не установлена, она будет заменена на пустую строку.

### Файлы

Используйте `{file:path/to/file}` для подстановки содержимого файла:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["./custom-instructions.md"],
  "provider": {
    "openai": {
      "options": {
        "apiKey": "{file:~/.secrets/openai-key}"
      }
    }
  }
}
```

Пути к файлам могут быть:
*   Относительными к директории конфигурационного файла
*   Или абсолютными путями, начинающимися с `/` или `~`

Это полезно для:
*   Хранения чувствительных данных, таких как API ключи, в отдельных файлах.
*   Включения больших файлов инструкций без загромождения вашего конфига.
*   Шаринга общих фрагментов конфигурации между несколькими конфигурационными файлами.

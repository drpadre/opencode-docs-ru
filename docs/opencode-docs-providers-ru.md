# Провайдеры (Providers)

Использование любого провайдера LLM в OpenCode.

## Учетные данные (Credentials)

Когда вы добавляете API-ключи провайдера с помощью команды `/connect`, они сохраняются в `~/.local/share/opencode/auth.json`.

```bash
/connect
~/.local/share/opencode/auth.json
```

## Конфигурация (Config)

Вы можете настроить провайдеров через секцию `provider` в вашей конфигурации OpenCode.

### Base URL

Вы можете настроить базовый URL для любого провайдера, установив опцию `baseURL`. Это полезно при использовании прокси-сервисов или пользовательских эндпоинтов.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": {
        "baseURL": "https://api.anthropic.com/v1"
      }
    }
  }
}
```

## OpenCode Zen

[OpenCode Zen](opencode-docs-zen-ru.md) — это список моделей, предоставляемый командой OpenCode, которые были протестированы и проверены на предмет хорошей работы с OpenCode.

> **Совет**: Если вы новичок, мы рекомендуем начать с OpenCode Zen.

1.  Запустите команду `/connect` в TUI, выберите `opencode` и перейдите на [opencode.ai/auth](https://opencode.ai/auth).
2.  Войдите в систему, добавьте данные для оплаты и скопируйте свой API-ключ.
3.  Запустите `/models` в TUI, чтобы увидеть список рекомендуемых нами моделей.

Это работает как любой другой провайдер в OpenCode. И его использование абсолютно необязательно.

## Каталог провайдеров

Давайте рассмотрим некоторые провайдеры подробно.

### Amazon Bedrock

Чтобы использовать Amazon Bedrock с OpenCode:

1.  Перейдите в каталог моделей (Model catalog) в консоли Amazon Bedrock и запросите доступ к моделям, которые вы хотите использовать.
    > **Совет**: Вам нужен доступ к модели в Amazon Bedrock.

2.  Настройте аутентификацию одним из следующих способов:

    *   **Переменные окружения (Быстрый старт)**
        Установите одну из этих переменных окружения при запуске `opencode`:
        ```bash
        # Вариант 1: Использование ключей доступа AWS
        AWS_ACCESS_KEY_ID=XXX AWS_SECRET_ACCESS_KEY=YYY opencode 
        
        # Вариант 2: Использование именованного профиля AWS
        AWS_PROFILE=my-profile opencode 
        
        # Вариант 3: Использование bearer токена Bedrock
        AWS_BEARER_TOKEN_BEDROCK=XXX opencode
        ```

    *   **Файл конфигурации (Рекомендуется)**
        Для специфичной для проекта или постоянной конфигурации используйте `opencode.json`:

        ```json
        {
          "$schema": "https://opencode.ai/config.json",
          "provider": {
            "amazon-bedrock": {
              "options": {
                "region": "us-east-1",
                "profile": "my-aws-profile"
              }
            }
          }
        }
        ```

3.  Запустите команду `/models`, чтобы выбрать нужную модель.

**Методы аутентификации**:
*   `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY`
*   `AWS_PROFILE`
*   `AWS_BEARER_TOKEN_BEDROCK`

### Anthropic

Мы рекомендуем подписаться на [Claude Pro](https://www.anthropic.com/news/claude-pro) или [Max](https://www.anthropic.com/max).

1.  После регистрации запустите команду `/connect` и выберите Anthropic.
2.  Здесь вы можете выбрать опцию Claude Pro/Max, и откроется браузер с просьбой аутентифицироваться.
3.  Теперь все модели Anthropic должны быть доступны при использовании команды `/models`.

#### Использование API-ключей
Вы также можете выбрать "Create an API Key", если у вас нет подписки Pro/Max. Или, если у вас уже есть API-ключ, выберите "Manually enter API Key" и вставьте его.

### Azure OpenAI

1.  Создайте ресурс Azure OpenAI на портале Azure. Вам понадобятся:
    *   **Resource name**: Часть вашего API эндпоинта (https://RESOURCE_NAME.openai.azure.com/)
    *   **API key**: KEY 1 или KEY 2
2.  Перейдите в [Azure AI Foundry](https://ai.azure.com/) и разверните модель.
    > **Примечание**: Имя развертывания должно совпадать с именем модели.
3.  Запустите `/connect` и найдите Azure.
4.  Введите ваш API-ключ.
5.  Установите имя ресурса как переменную окружения:
    ```bash
    AZURE_RESOURCE_NAME=XXX opencode
    ```

### Azure Cognitive Services

Аналогично Azure OpenAI, но используйте `AZURE_COGNITIVE_SERVICES_RESOURCE_NAME`.

### Baseten

1.  Получите API-ключ на [Baseten](https://app.baseten.co/).
2.  Запустите `/connect`, найдите Baseten и введите ключ.

### Cerebras

1.  Получите API-ключ в [консоли Cerebras](https://inference.cerebras.ai/).
2.  Запустите `/connect`, найдите Cerebras и введите ключ.

### Cloudflare AI Gateway

1.  Создайте шлюз в [панели Cloudflare](https://dash.cloudflare.com/).
2.  Установите Account ID и Gateway ID как переменные окружения:
    ```bash
    export CLOUDFLARE_ACCOUNT_ID=...
    export CLOUDFLARE_GATEWAY_ID=...
    ```
3.  Запустите `/connect`, найдите Cloudflare AI Gateway и введите API токен.

### Cortecs

1.  Получите API-ключ в [консоли Cortecs](https://cortecs.ai/).
2.  Запустите `/connect`, найдите Cortecs и введите ключ.

### DeepSeek

1.  Получите API-ключ в [консоли DeepSeek](https://platform.deepseek.com/).
2.  Запустите `/connect`, найдите DeepSeek и введите ключ.

### Deep Infra

1.  Получите API-ключ на [Deep Infra](https://deepinfra.com/dash).
2.  Запустите `/connect` и введите ключ.

### Fireworks AI

1.  Получите API-ключ в [консоли Fireworks AI](https://app.fireworks.ai/).
2.  Запустите `/connect` и введите ключ.

### GitHub Copilot

1.  Запустите `/connect` и найдите GitHub Copilot.
2.  Перейдите на `github.com/login/device` и введите код.

### Google Vertex AI

1.  Убедитесь, что у вас включен Vertex AI API в Google Cloud.
2.  Установите переменные окружения:
    *   `GOOGLE_CLOUD_PROJECT`
    *   `VERTEX_LOCATION` (опционально, по умолчанию global)
    *   `GOOGLE_APPLICATION_CREDENTIALS` (путь к JSON-ключу) ИЛИ аутентифицируйтесь через `gcloud auth application-default login`.
3.  Запустите `/models` для выбора модели.

### Groq

1.  Получите API-ключ в [консоли Groq](https://console.groq.com/).
2.  Запустите `/connect` и введите ключ.

### Hugging Face

1.  Создайте токен с правами на Inference Providers в настройках Hugging Face.
2.  Запустите `/connect` и введите токен.

### Helicone

[Helicone](https://helicone.ai) — это платформа наблюдаемости LLM.
1.  Получите API-ключ на Helicone.
2.  Запустите `/connect` и введите ключ.

Вы можете настроить пользовательские заголовки для Helicone в конфиге:

```json
"headers": {
  "Helicone-Cache-Enabled": "true",
  "Helicone-User-Id": "opencode"
}
```

### llama.cpp

Вы можете использовать локальные модели через утилиту `llama-server`.

Конфигурация:
```json
{
  "provider": {
    "llama.cpp": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "llama-server (local)",
      "options": { "baseURL": "http://127.0.0.1:8080/v1" },
      "models": { ... }
    }
  }
}
```

### IO.NET

1.  Получите API-ключ в [консоли IO.NET](https://ai.io.net/).
2.  Запустите `/connect` и введите ключ.

### LM Studio

Используйте `lmstudio` как пользовательский провайдер с `baseURL` pointing to `http://127.0.0.1:1234/v1`.

### Moonshot AI

1.  Получите API-ключ в [консоли Moonshot AI](https://platform.moonshot.ai/console).
2.  Запустите `/connect` и введите ключ.

### MiniMax

1.  Получите API-ключ в [консоли MiniMax](https://platform.minimax.io/login).
2.  Запустите `/connect` и введите ключ.

### Nebius Token Factory

1.  Получите API-ключ в [консоли Nebius](https://tokenfactory.nebius.com/).
2.  Запустите `/connect` и введите ключ.

### Ollama

Вы можете использовать локальные модели через Ollama.

```json
{
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (local)",
      "options": { "baseURL": "http://localhost:11434/v1" },
      "models": { "llama2": { "name": "Llama 2" } }
    }
  }
}
```

> **Совет**: Если вызовы инструментов не работают, попробуйте увеличить `num_ctx` в Ollama.

### Ollama Cloud

1.  Получите API-ключ на [ollama.com](https://ollama.com/).
2.  Запустите `/connect`.
3.  **Важно**: Вы должны скачать информацию о модели локально: `ollama pull gpt-oss:20b-cloud`.

### OpenAI

1.  Получите API-ключ на [OpenAI Platform](https://platform.openai.com/api-keys).
2.  Запустите `/connect`.

### OpenRouter

1.  Получите API-ключ на [OpenRouter](https://openrouter.ai/settings/keys).
2.  Запустите `/connect`.

### SAP AI Core

1.  Получите сервисный ключ (service key) в SAP BTP Cockpit.
2.  Запустите `/connect` и введите JSON ключа.

### OVHcloud AI Endpoints

1.  Получите API-ключ в панели OVHcloud.
2.  Запустите `/connect`.

### Together AI

1.  Получите API-ключ в [консоли Together AI](https://api.together.ai).
2.  Запустите `/connect`.

### Venice AI

1.  Получите API-ключ в [консоли Venice AI](https://venice.ai).
2.  Запустите `/connect`.

### Vercel AI Gateway

1.  Получите API-ключ в [Vercel dashboard](https://vercel.com/).
2.  Запустите `/connect`.

### xAI

1.  Получите API-ключ в [консоли xAI](https://console.x.ai/).
2.  Запустите `/connect`.

### Z.AI

1.  Получите API-ключ в [консоли Z.AI](https://z.ai/manage-apikey/apikey-list).
2.  Запустите `/connect`.

### ZenMux

1.  Получите API-ключ в [ZenMux dashboard](https://zenmux.ai/settings/keys).
2.  Запустите `/connect`.

## Пользовательский провайдер (Custom provider)

Чтобы добавить любого OpenAI-совместимого провайдера, которого нет в списке `/connect`:

1.  Запустите `/connect` и выберите **Other**.
2.  Введите уникальный ID для провайдера (например, `myprovider`).
3.  Введите API-ключ.
4.  Обновите ваш `opencode.json`:

    ```json
    {
      "provider": {
        "myprovider": {
          "npm": "@ai-sdk/openai-compatible",
          "name": "My AI Provider",
          "options": {
            "baseURL": "https://api.myprovider.com/v1"
          },
          "models": {
            "my-model-name": { "name": "My Model Display Name" }
          }
        }
      }
    }
    ```

## Устранение неполадок

Если у вас проблемы с настройкой провайдера:

1.  Проверьте настройку аутентификации: `opencode auth list`.
2.  Для пользовательских провайдеров убедитесь, что:
    *   ID провайдера в `/connect` совпадает с ID в конфиге.
    *   Используется правильный npm пакет (`@ai-sdk/openai-compatible`).
    *   Указан правильный `baseURL`.

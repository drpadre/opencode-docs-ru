# Модели (Models)

Настройка LLM провайдера и модели.

## Провайдеры (Providers)

Большинство популярных провайдеров загружены по умолчанию. Если вы добавили учетные данные через команду `/connect`, они будут доступны при запуске OpenCode.

## Выбор модели (Select a model)
После настройки провайдера вы можете выбрать модель, введя:
```bash
/models
```

## Рекомендуемые модели (Recommended models)

Несколько моделей, которые хорошо работают с OpenCode (генерация кода + вызов инструментов):
*   GPT 5.2
*   GPT 5.1 Codex
*   Claude Opus 4.5
*   Claude Sonnet 4.5
*   Minimax M2.1
*   Gemini 3 Pro

## Установка модели по умолчанию (Set a default)

В `opencode.json`:
```json
{
  "model": "anthropic/claude-sonnet-4.5"
}
```
Формат: `provider_id/model_id`.
Например, для Zen: `opencode/gpt-5.1-codex`.

## Настройка моделей (Configure models)

Вы можете глобально настроить параметры модели:

```json
{
  "provider": {
    "openai": {
      "models": {
        "gpt-5": {
          "options": {
            "reasoningEffort": "high"
          }
        }
      }
    }
  }
}
```

## Варианты (Variants)

Многие модели поддерживают несколько вариантов с разными конфигурациями. OpenCode поставляется со встроенными вариантами по умолчанию.

### Встроенные варианты
*   **Anthropic**: `high` (default), `max`.
*   **OpenAI**: `none`, `minimal`, `low`, `medium`, `high`, `xhigh`.
*   **Google**: `low`, `high`.

### Пользовательские варианты
Вы можете переопределить существующие варианты или добавить свои:

```json
{
  "provider": {
    "openai": {
      "models": {
        "gpt-5": {
          "variants": {
            "thinking": { "reasoningEffort": "high" },
            "fast": { "disabled": true }
          }
        }
      }
    }
  }
}
```

### Переключение вариантов
Используйте привязку клавиш `variant_cycle` для быстрого переключения между вариантами.

## Загрузка моделей (Loading models)

Порядок приоритета при запуске OpenCode:
1.  Флаг командной строки `--model` или `-m`.
2.  Модель в конфиге OpenCode (`"model": "..."`).
3.  Последняя использованная модель.
4.  Первая модель по внутреннему приоритету.

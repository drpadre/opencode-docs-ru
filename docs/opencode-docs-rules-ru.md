# Правила (Rules)

Установите пользовательские инструкции для opencode.

## Инициализация (Initialize)

Чтобы создать новый файл `AGENTS.md`, вы можете запустить команду `/init` в opencode.

```bash
/init
```
> **Совет**: Вам следует закоммитить файл `AGENTS.md` вашего проекта в Git.

Эта команда просканирует ваш проект и все его содержимое, чтобы понять, о чем проект, и сгенерирует файл `AGENTS.md`. Это помогает opencode лучше ориентироваться в проекте.
Если у вас уже есть файл `AGENTS.md`, она попытается добавить информацию в него.

## Пример (Example)

Вы также можете просто создать этот файл вручную.

```markdown
# SST v3 Monorepo Project
This is an SST v3 monorepo with TypeScript. The project uses bun workspaces for package management.

## Project Structure
- `packages/` - Contains all workspace packages (functions, core, web, etc.)
- `infra/` - Infrastructure definitions split by service (storage.ts, api.ts, web.ts)
- `sst.config.ts` - Main SST configuration with dynamic imports

## Code Standards
- Use TypeScript with strict mode enabled
- Shared code goes in `packages/core/` with proper exports configuration
```

## Типы (Types)

Opencode поддерживает чтение файла `AGENTS.md` из нескольких мест.

### Проект (Project)
Как показано выше, где `AGENTS.md` размещен в корне проекта. Это правила, специфичные для проекта.

### Глобальные (Global)
Вы также можете иметь глобальные правила в файле `~/.config/opencode/AGENTS.md`. Они применяются ко всем сессиям opencode.

Поскольку этот файл не коммитится в Git, мы рекомендуем использовать его для указания личных правил, которым должна следовать LLM.

## Приоритет (Precedence)

При запуске opencode ищет файлы в следующем порядке:
1.  Локальные файлы, поднимаясь вверх от текущей директории.
2.  Глобальный файл в `~/.config/opencode/AGENTS.md`.

Если у вас есть и глобальные, и проектные правила, opencode объединит их.

## Пользовательские инструкции (Custom Instructions)

Вы можете указать файлы пользовательских инструкций в вашем `opencode.json` или глобальном `~/.config/opencode/opencode.json`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": [
    "CONTRIBUTING.md",
    "docs/guidelines.md",
    ".cursor/rules/*.md"
  ]
}
```

Все файлы инструкций объединяются с вашими файлами `AGENTS.md`.

## Ссылка на внешние файлы (Referencing External Files)

Хотя opencode не анализирует ссылки на файлы в `AGENTS.md` автоматически, вы можете достичь аналогичной функциональности.

### Использование opencode.json

Рекомендуемый подход — использовать поле `instructions` в `opencode.json`.

```json
{
  "instructions": [
    "docs/development-standards.md", 
    "packages/*/AGENTS.md"
  ]
}
```

### Ручные инструкции в AGENTS.md

Вы можете научить opencode читать внешние файлы, предоставив явные инструкции в вашем `AGENTS.md`.

```markdown
# TypeScript Project Rules
## External File Loading
CRITICAL: When you encounter a file reference (e.g., @rules/general.md), use your Read tool to load it on a need-to-know basis.

## Development Guidelines
For TypeScript code style and best practices: @docs/typescript-guidelines.md
```

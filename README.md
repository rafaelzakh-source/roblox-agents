# roblox-agents

Команда ИИ-агентов Claude Code для разработки игр на Roblox (плагин `roblox-team`).

| Агент | Роль | Что делает |
|---|---|---|
| `roblox-analyst` | смотрит | Разбирает проект: структура, сервер/клиент, RemoteEvents, сохранения. Ничего не меняет |
| `roblox-designer` | создаёт | Механики, прогрессия, экономика, монетизация → дизайн-док и план задач |
| `roblox-builder` | делает | Пишет Luau-код: скрипты, UI, Remotes, DataStore |
| `roblox-reviewer` | проверяет код | Баги, эксплойты, утечки, ошибки сохранения |
| `roblox-tester` | проверяет игру | Тесты и чек-лист проверки в Studio |
| `roblox-polisher` | дорабатывает | Исправляет замечания, UI/UX, анимации, телефон, производительность |

Скилл `roblox-pipeline` задаёт порядок: **смотрит → создаёт → делает → проверяет → тестирует → дорабатывает**.

## Как подключить к игре

### Вариант А — автоматически (рекомендуется, работает и в облачных сессиях)
В репозитории игры создай файл `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "roblox-agents": {
      "source": { "source": "github", "repo": "rafaelzakh-source/roblox-agents" }
    }
  },
  "enabledPlugins": {
    "roblox-team@roblox-agents": true
  }
}
```

### Вариант Б — вручную в Claude Code
```
/plugin marketplace add rafaelzakh-source/roblox-agents
/plugin install roblox-team@roblox-agents
```

## Как пользоваться
Просто пиши задачу: «добавь магазин скинов», «найди, почему не сохраняются монеты», «доработай интерфейс под телефон». Claude сам раздаст работу агентам. Можно вызвать агента напрямую: «попроси roblox-reviewer проверить последние изменения».

## Как менять агентов
Каждый агент — файл `plugins/roblox-team/agents/<имя>.md`: сверху настройки (`name`, `description`, `tools`), ниже — инструкция. После изменения подними `version` в `plugins/roblox-team/.claude-plugin/plugin.json`.

# roblox-agents

Команда ИИ-агентов Claude Code для разработки игр на Roblox (плагин `roblox-team`).

| Агент | Роль | Что делает |
|---|---|---|
| `roblox-lorekeeper` | хранитель знаний | Ищет нужное в Obsidian-хранилище игры, даёт контекст и план раздачи задач, записывает итоги обратно |
| `roblox-analyst` | смотрит | Разбирает проект: структура, сервер/клиент, RemoteEvents, сохранения. Ничего не меняет |
| `roblox-designer` | создаёт | Механики, прогрессия, экономика, монетизация → дизайн-док и план задач |
| `roblox-builder` | делает | Пишет Luau-код: скрипты, UI, Remotes, DataStore |
| `roblox-studio-operator` | руки в Studio | Работает с открытым Studio через MCP: Explorer, свойства, Play-тест, Output |
| `roblox-model-fixer` | чинит модели | Почему модель не вставляется, разваливается, не того размера — и исправляет |
| `roblox-asset-finder` | ищет ассеты | Модели, звуки, текстуры с проверкой лицензий и бэкдоров |
| `roblox-ui-designer` | интерфейс | Меню, HUD, магазин — удобно на телефоне, в едином стиле |
| `roblox-level-builder` | уровни | Карта, маршрут игрока, рельеф, освещение, спавны |
| `roblox-economy-balancer` | баланс | Цены, награды, прогрессия — с расчётами и таблицами |
| `roblox-engagement-designer` | удержание | Психология мотивации: первые 60 секунд, цели, награды, события, честная монетизация, метрики D1/D7/D30 |
| `roblox-vfx-sound` | эффекты | Частицы, звуки, анимации, «сочность» |
| `roblox-debugger` | ищет причину бага | Разбирает ошибки Output, находит корневую причину |
| `roblox-reviewer` | проверяет код | Баги, эксплойты, утечки, ошибки сохранения |
| `roblox-tester` | проверяет игру | Тесты и чек-лист проверки в Studio |
| `roblox-polisher` | дорабатывает | Исправляет замечания, UI/UX, телефон, производительность |
| `roblox-publisher` | релиз | Проверка перед публикацией: правила Roblox, монетизация, страница игры |

Скилл `roblox-pipeline` задаёт порядок работы и маршруты. Каждая задача начинается и заканчивается с `roblox-lorekeeper`.

## Obsidian-хранилище
Добавь в `CLAUDE.md` репозитория игры строку с путём к хранилищу:

```
Obsidian-хранилище: C:\Users\Имя\Documents\МояИгра
```

Для облачных сессий хранилище должно лежать в GitHub (плагин Obsidian Git) и быть подключено к сессии.

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

## Как обновить у себя
```
/plugin marketplace update roblox-agents
```
```
/plugin update roblox-team@roblox-agents
```
Потом начни новый чат. Или включи автообновление: `/plugin` → Marketplaces → roblox-agents → Enable auto-update.

## Как менять агентов
Каждый агент — файл `plugins/roblox-team/agents/<имя>.md`: сверху настройки (`name`, `description`, `tools`), ниже — инструкция. После изменения подними `version` в `plugins/roblox-team/.claude-plugin/plugin.json`.

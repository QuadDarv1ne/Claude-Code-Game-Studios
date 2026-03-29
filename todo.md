# TODO — Claude Code Game Studios

## 🔴 Критические исправления

### 1. Несогласованность количества навыков
- **Проблема**: В README_RU.md бейдж показывает "37 Skills", но фактически 42 навыка
- **Файл**: `README_RU.md` (строка с бейджем)
- **Решение**: Изменить бейдж с `37-green` на `42-green`

### 2. Несогласованность в структуре проекта
- **Проблема**: В разделе "Структура проекта" указано "37 slash-команд", должно быть 42
- **Файл**: `README_RU.md`
- **Решение**: Исправить комментарий в блоке структуры

---

## 🟡 Улучшения качества

### 3. Тестирование новых навыков
- **Задача**: Протестировать каждый из 5 новых навыков в реальной работе
- **Навыки**:
  - `/monetization-design` — проверить генерацию economy-balance.csv
  - `/tutorial-flow` — проверить создание Mermaid-диаграмм
  - `/analytics-setup` — проверить генерацию шаблона AnalyticsService
  - `/narrative-design` — проверить диалоговые деревья
  - `/ui-ux-review` — проверить интеграцию с accessibility-specialist
- **Критерий**: Каждый навык должен работать без ошибок и создавать файлы

### 4. Валидация хуков для новых навыков
- **Задача**: Убедиться, что хуки корректно работают с новыми файлами навыков
- **Хуки**: `validate-commit.sh`, `log-agent.sh`
- **Тест**: Запустить коммит с изменениями в новых навыках

### 5. Консистентность стиля навыков
- **Проблема**: Новые навыки могут отличаться по структуре от существующих
- **Задача**: Сравнить с эталонными (`brainstorm`, `code-review`, `sprint-plan`)
- **Критерий**: Единый формат frontmatter, фаз, AskUserQuestion интеграции

---

## 🟢 Долгосрочные улучшения

### 6. Добавить шаблоны для новых навыков
- **monetization-design**: Шаблон `monetization-plan.md` в `.claude/docs/templates/`
- **tutorial-flow**: Шаблон `ftue-flow.md` в `.claude/docs/templates/`
- **analytics-setup**: Шаблон `event-catalog.md` в `.claude/docs/templates/`
- **narrative-design**: Шаблон `dialogue-tree.md` в `.claude/docs/templates/`
- **ui-ux-review**: Шаблон `ui-audit-report.md` в `.claude/docs/templates/`

### 7. Интеграция с агентами
- **Задача**: Добавить ссылки на новые навыки в соответствующих агентов
- **Агенты**:
  - `economy-designer.md` → `/monetization-design`
  - `ux-designer.md` → `/ui-ux-review`
  - `narrative-director.md` → `/narrative-design`
  - `analytics-engineer.md` → `/analytics-setup`
  - `game-designer.md` → `/tutorial-flow`

### 8. Обновить документацию координации
- **Файл**: `.claude/docs/agent-coordination-map.md`
- **Задача**: Добавить пути эскалации для новых навыков

---

## 📋 Проверка перед merge в main

- [ ] Исправлен бейдж с количеством навыков (37→42)
- [ ] Исправлен комментарий в структуре проекта
- [ ] Все 5 новых навыков протестированы
- [ ] Хуки проходят валидацию
- [ ] Стиль навыков консистентен с существующими
- [ ] Git status чист (нет незакоммиченных изменений)
- [ ] Запущен `git diff main..dev` — все изменения ожидаются
- [ ] Создан pull request или прямой merge после проверки

---

## 🔄 Активные изменения (dev)

| Файл | Статус | Примечание |
|------|--------|------------|
| `.claude/skills/monetization-design/SKILL.md` | ✅ Создан | Ожидает тестирования |
| `.claude/skills/tutorial-flow/SKILL.md` | ✅ Создан | Ожидает тестирования |
| `.claude/skills/analytics-setup/SKILL.md` | ✅ Создан | Ожидает тестирования |
| `.claude/skills/narrative-design/SKILL.md` | ✅ Создан | Ожидает тестирования |
| `.claude/skills/ui-ux-review/SKILL.md` | ✅ Создан | Ожидает тестирования |
| `.claude/docs/skills-reference.md` | ✅ Обновлён | Добавлены 5 навыков |
| `README.md` | ✅ Обновлён | 37→42 навыка |
| `README_RU.md` | ⚠️ Требует исправления | Бейдж не обновлён |
| `todo.md` | ✅ Создан | Этот файл |

---

*Последнее обновление: 29.03.2026*

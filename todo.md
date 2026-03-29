# TODO — Claude Code Game Studios

## ✅ Выполнено

- [x] Бейдж навыков исправлен (37→42) в README_RU.md
- [x] Комментарий в структуре проекта исправлен (37→42)
- [x] 5 новых навыков созданы и закоммичены
- [x] README_RU.md создан
- [x] Изменения отправлены в main
- [x] Заголовок в README_RU.md исправлен (42 рабочих процесса)
- [x] 5 шаблонов добавлены (.claude/docs/templates/)
- [x] Новые навыки интегрированы в 5 агентов
- [x] agent-coordination-map.md обновлён

---

## 🟡 Улучшения качества

### 1. Тестирование новых навыков
- **Задача**: Протестировать каждый из 5 новых навыков в реальной работе
- **Навыки**:
  - `/monetization-design` — проверить генерацию economy-balance.csv
  - `/tutorial-flow` — проверить создание Mermaid-диаграмм
  - `/analytics-setup` — проверить генерацию шаблона AnalyticsService
  - `/narrative-design` — проверить диалоговые деревья
  - `/ui-ux-review` — проверить интеграцию с accessibility-specialist
- **Критерий**: Каждый навык должен работать без ошибок и создавать файлы

### 2. Валидация хуков для новых навыков
- **Задача**: Убедиться, что хуки корректно работают с новыми файлами навыков
- **Хуки**: `validate-commit.sh`, `log-agent.sh`
- **Тест**: Запустить коммит с изменениями в новых навыках

### 3. Консистентность стиля навыков
- **Проблема**: Новые навыки могут отличаться по структуре от существующих
- **Задача**: Сравнить с эталонными (`brainstorm`, `code-review`, `sprint-plan`)
- **Критерий**: Единый формат frontmatter, фаз, AskUserQuestion интеграции

---

## 🟢 Долгосрочные улучшения

### 4. Обновить документацию координации
- **Файл**: `.claude/docs/agent-coordination-map.md`
- **Задача**: Добавить пути эскалации для новых навыков
- **Статус**: ✅ Выполнено — добавлена секция Skills Integration

---

## 📋 Проверка перед merge в main

- [x] Исправлен заголовок в README_RU.md (37→42 рабочих процесса)
- [x] 5 шаблонов добавлены
- [x] Агенты обновлены (5 файлов)
- [x] agent-coordination-map.md обновлён
- [ ] Все 5 новых навыков протестированы
- [ ] Хуки проходят валидацию
- [ ] Стиль навыков консистентен с существующими
- [ ] Git status чист (нет незакоммиченных изменений)
- [ ] Запущен `git diff main..dev` — все изменения ожидаются

---

## 🔄 Активные изменения (dev)

| Файл | Статус | Примечание |
|------|--------|------------|
| `.claude/docs/templates/monetization-plan.md` | ✅ Создан | Шаблон плана монетизации |
| `.claude/docs/templates/ftue-flow.md` | ✅ Создан | Шаблон FTUE |
| `.claude/docs/templates/event-catalog.md` | ✅ Создан | Каталог событий |
| `.claude/docs/templates/dialogue-tree.md` | ✅ Создан | Диалоговые деревья |
| `.claude/docs/templates/ui-audit-report.md` | ✅ Создан | UI/UX аудит |
| `.claude/agents/economy-designer.md` | ✅ Обновлён | +Related Skills |
| `.claude/agents/ux-designer.md` | ✅ Обновлён | +Related Skills |
| `.claude/agents/narrative-director.md` | ✅ Обновлён | +Related Skills |
| `.claude/agents/analytics-engineer.md` | ✅ Обновлён | +Related Skills |
| `.claude/agents/game-designer.md` | ✅ Обновлён | +Related Skills |
| `.claude/docs/agent-coordination-map.md` | ✅ Обновлён | +Skills Integration |

---

## 📚 Документация проекта

Полная документация доступна в проекте:

| Файл | Описание |
|------|----------|
| `.claude/docs/quick-start.md` | Быстрый старт — иерархия агентов, команды, шаблоны |
| `.claude/docs/setup-requirements.md` | Требования к окружению (Git, Claude Code, jq, Python) |
| `docs/WORKFLOW-GUIDE.md` | Полное руководство по всем фазам разработки (0-10) |
| `CLAUDE.md` | Главная конфигурация проекта |
| `.claude/docs/skills-reference.md` | Все 42 slash-команды |
| `.claude/docs/agent-roster.md` | Все 48 агентов с областями |

---

*Последнее обновление: 29.03.2026*

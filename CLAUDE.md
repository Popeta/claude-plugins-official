# CLAUDE.md — claude-plugins-official (форк)

**Что это:** форк официальной директории плагинов Claude Code. Содержит патчи для Telegram plugin (idle-survive + first-wins logic), которые НЕ должны потеряться при мерже upstream.

## Правила работы

- **Глобальные правила:** `~/.claude/CLAUDE.md`
- **Язык ответов:** русский

## ⚠️ КРИТИЧНО: синхронизация с upstream

Память: `~/.claude/projects/-Users-vitalijpopeta-Desktop-dev-VP/memory/project_telegram_plugin_fork.md`

При мерже `upstream/main`:

1. `git fetch upstream && git show upstream/main:external_plugins/telegram/.claude-plugin/plugin.json | grep version` — проверить версию
2. **Если version > 0.0.7** — мержить upstream/main
3. **ПРОВЕРИТЬ** что наши фиксы НЕ вернулись в состояние upstream:
   - orphan watchdog НЕ вернулся
   - stdin-close handlers НЕ вернулись
   - new-kills-old logic НЕ вернулся
   - Наши idle-survive + first-wins должны сохраниться
4. Обновить симлинк `~/.claude/plugins/cache/.../<new>/server.ts` → форк
5. Пушнуть

**Запуск чек-листа:** команда "неделя" в VP (пункт 11 — "Telegram plugin fork check")

## Скилл для форка

- `~/.claude/skills/fork-sync-upstream` — общий workflow для синхронизации любых форков с diverged upstream

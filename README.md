# Release Notify Action

GitHub Action для отправки уведомлений о релизах в Mattermost с форматированием ссылок Linear и GitHub PR.

## Описание

Этот action получает данные о коммитах и отправляет красиво отформатированные уведомления о релизах в Mattermost. Поддерживает автоматическое форматирование ссылок на задачи Linear и GitHub Pull Requests.

## Возможности

- 📢 Отправка уведомлений о релизах в Mattermost
- 🔗 Автоматическое форматирование ссылок Linear (DEV-, FEA-, INT-, PRT-, SUP-, MULT-)
- 🔗 Автоматическое форматирование ссылок GitHub PR (#123)
- 🎨 Настраиваемый цвет сообщений
- 📦 Поддержка ссылок на container registry
- 🛠️ Гибкая настройка через параметры

## Использование

```yaml
- name: Send release notification
  uses: cyberc00n/relese-notify-action@v1
  with:
    tag: ${{ github.ref_name }}
    mattermost-url: ${{ secrets.MATTERMOST_WEBHOOK_URL }}
    repo-name: 'My Project'
    registry-url: 'https://ghcr.io'
    color: '#00ff00'
    linear-enabled: 'true'
    linear-workspace: 'myworkspace'
    github-pr-enabled: 'true'
```

## Входные параметры

| Параметр | Описание | Обязательный | По умолчанию |
|----------|----------|--------------|--------------|
| `tag` | Тег/версия релиза | ✅ | - |
| `mattermost-url` | URL webhook Mattermost | ✅ | - |
| `repo-name` | Отображаемое имя репозитория | ❌ | `${{ github.repository }}` |
| `registry-url` | URL container registry | ❌ | `''` |
| `color` | Цвет левой границы сообщения | ❌ | `'#58FF33'` |
| `linear-enabled` | Включить форматирование ссылок Linear | ❌ | `'true'` |
| `linear-workspace` | Имя workspace Linear | ❌ | `'binomtracker'` |
| `github-pr-enabled` | Включить форматирование ссылок GitHub PR | ❌ | `'true'` |
| `custom-commit-title` | Пользовательский заголовок коммита | ❌ | `''` |

## Выходные параметры

| Параметр | Описание |
|----------|----------|
| `formatted-message` | Отформатированное сообщение коммита |
| `commit-title` | Оригинальный заголовок коммита |

## Примеры форматирования

### Linear задачи
```
Исходный текст: "Fix DEV-123 issue"
Результат: "Fix <https://linear.app/myworkspace/issue/DEV-123|DEV-123> issue"
```

### GitHub PR
```
Исходный текст: "Feature implementation (#456)"
Результат: "Feature implementation <https://github.com/user/repo/pull/456|#456>"
```

## Пример workflow

```yaml
name: Release Notification

on:
  release:
    types: [published]

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        
      - name: Send notification
        uses: cyberc00n/relese-notify-action@v1
        with:
          tag: ${{ github.event.release.tag_name }}
          mattermost-url: ${{ secrets.MATTERMOST_WEBHOOK_URL }}
          repo-name: ${{ github.event.repository.name }}
          registry-url: 'https://ghcr.io'
```

## Настройка Mattermost

1. Создайте incoming webhook в Mattermost
2. Добавьте URL webhook в секреты GitHub как `MATTERMOST_WEBHOOK_URL`

## Лицензия

MIT

## Автор

cyberc00n 
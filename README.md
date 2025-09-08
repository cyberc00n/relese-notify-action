# Release Notify Action

GitHub Action for sending release notifications to Mattermost with automatic formatting of Linear task and GitHub PR links.

## Features

- 📝 Automatic retrieval of the last commit title
- 🔗 Linear task link formatting (DEV-123, FEA-456, etc.)
- 🔗 GitHub PR link formatting (#123)
- 🎨 Customizable message color
- 📦 Container registry URL display support
- ✅ JSON validation before sending

## Usage

```yaml
- uses: cyberc00n/relese-notify-action@v0.0.1
  with:
    tag: v1.20.3
    mattermost-url: ${{ secrets.MATTERMOST_WEBHOOK_URL }}
    repo-name: "My Project"
    registry-url: "us-docker.pkg.dev/my-project/registry"
    color: "#EF5D60"
    linear-enabled: true
    linear-workspace: "myworkspace"
    github-pr-enabled: true
```

## Parameters

| Parameter | Description | Required | Default |
|-----------|-------------|----------|---------|
| `tag` | Release tag/version | ✅ | - |
| `mattermost-url` | Mattermost webhook URL | ✅ | - |
| `repo-name` | Repository display name | ❌ | `${{ github.repository }}` |
| `registry-url` | Container registry URL | ❌ | `''` |
| `color` | Message left border color | ❌ | `#58FF33` |
| `linear-enabled` | Enable Linear link formatting | ❌ | `true` |
| `linear-workspace` | Linear workspace name | ❌ | `binomtracker` |
| `github-pr-enabled` | Enable GitHub PR link formatting | ❌ | `true` |
| `custom-commit-title` | Custom commit title | ❌ | `''` |

## Fixes

### v0.0.1
- ✅ Fixed "Failed to decode the payload" error when sending to Mattermost
- ✅ Added proper JSON escaping
- ✅ Added JSON validation before sending
- ✅ Improved special character handling in messages

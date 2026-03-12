# aicre8-skill

Agent skill for [aicre8.dev](https://aicre8.dev) — AI website builder.

## What is this?

This repo contains the [SKILL.md](./SKILL.md) file that allows AI agents (OpenClaw, Claude Code, Cursor, etc.) to discover and use aicre8.dev's API to build, edit, and deploy websites.

## Install

```bash
npx skills add AICre8dev/aicre8-skill
```

## What agents can do

| Skill | Description |
|-------|-------------|
| `create_project` | Build a website from a text prompt |
| `edit_project` | Modify an existing site with follow-up prompts |
| `upload_image` | Add logos, photos, and assets |
| `deploy_project` | Publish to `{slug}.aicre8.app` |
| `list_projects` | List all projects |
| `get_project` | Get project details and files |

## Auth

Get an API key at [aicre8.dev/settings/api-keys](https://aicre8.dev/settings/api-keys). Keys use `ak_live_` prefix.

## Links

- **Website**: [aicre8.dev](https://aicre8.dev)
- **Hosted skill**: [aicre8.dev/skill.md](https://aicre8.dev/skill.md)
- **Token launchpad**: [vybes.fun](https://vybes.fun) ([skill.md](https://vybes.fun/skill.md))

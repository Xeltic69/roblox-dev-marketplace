# roblox-dev marketplace

A Claude Code marketplace with one plugin, **roblox-dev**, by Xeltic69: Roblox game development for Claude Code with 22 commands for building, fixing, auditing, shipping and growing a game.

## Install

```text
/plugin marketplace add Xeltic69/roblox-dev-marketplace
/plugin install roblox-dev@roblox-dev-marketplace
```

For a local test without publishing:

```bash
claude --plugin-dir ./plugins/roblox-dev
```

## What you get

| Group | Commands |
| --- | --- |
| Understand | `onboard`, `full-audit`, `release-check`, `market-research` |
| Build | `new-game`, `add-feature`, `new-system`, `gameplay`, `combat`, `ui`, `world` |
| Fix and improve | `fix-bug`, `performance`, `save-data`, `economy`, `analytics` |
| Restructure and tidy | `backup`, `cleanup`, `refactor-system`, `restructure` |
| Grow | `growth`, `packaging` |

Run any of them as `/roblox-dev:<name>`, for example `/roblox-dev:full-audit security` or `/roblox-dev:fix-bug diagnose data not saving on leave`. Destructive or file-writing commands are user-invoked only, and nothing is published, purchased or deleted without your explicit yes.

**Full command reference with what each one does, examples and safety rules: [plugins/roblox-dev/README.md](plugins/roblox-dev/README.md).**

## Notes

License: MIT ([LICENSE](LICENSE)). Roblox and other game names mentioned in the documentation are trademarks of their respective owners; this project is not affiliated with or endorsed by Roblox Corporation.

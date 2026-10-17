---
name: save-data
description: Design, review or fix Roblox player data persistence: saving, session ownership, retries, migrations. Use when the user mentions DataStore, saving, loading or data loss.
argument-hint: "<data task>"
---

# /roblox-dev:save-data

Task: $ARGUMENTS (if empty, ask what data and what problem, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/persistence.md, ../roblox-dev/references/networking-security.md.

- Read the existing save code and schema first; list every key and field in use.
- **Ask before changing any existing key or schema.** Write versioned, reversible migrations; never run a migration against live or published data; test on a copy or fresh key; report the rollback path.
- Cover session ownership, load-failure handling (never overwrite good data after a failed load), save on leave and on shutdown, retries with backoff, and access to data only through the owning system's API.

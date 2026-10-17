# Source control, sync, packages, CI and Open Cloud

Inspect existing repository rules, tool manifests, project mappings and generated files. Determine which source owns scripts/assets before editing: filesystem-managed, Studio-managed or explicitly hybrid. Do not let Studio edits fight live sync or patch generated output instead of its source.

For Rojo projects, read current [sync details](https://rojo.space/docs/v7/sync-details/) and the installed project format. File-to-instance mapping and live-sync limits matter to persistence of edits. Preserve paths, mappings, package realms and asset handling. Treat a current project's pinned tool version as authoritative rather than a generic version table.

Dependencies should solve a concrete need. Check actual package API/runtime context, version, license and maintenance evidence; preserve lockfiles. [Wally](https://github.com/UpliftGames/wally) documents manifests and resolved dependencies. Other package/tool managers are valid when already used. Do not add a networking generator, ECS, React/Fusion, service framework or profile library only because a guide mentions it.

Use Git or the project's version mechanism for recoverable code changes. Studio/cloud workflows do not justify a universal prohibition on committing Luau. Preserve user edits and keep scope-specific diffs reviewable. A broad migration needs source backups, compatibility and rollback planning, not a destructive overwrite.

CI should validate relevant syntax/types/tests/builds with project tools. Type-checking does not demonstrate client behavior, durable purchases or visual correctness. Run external/cloud workflows only within authorized scope and with isolated service targets. Do not download or run remote installers without approval.

When no toolchain exists and the requested screen/system is small, native Studio development remains valid. Offline source delivery should identify exact services/script types/init path without making setup a hidden prerequisite.

## Common tools and checks (verify versions in the project)

Typical Roblox toolchain pieces: Rojo (filesystem sync), Wally (packages), Selene (linter), StyLua (formatter), Rokit or Aftman (tool version manager), Lune (standalone Luau scripts for tooling and tests). Use what the project already pins; do not introduce a new one without a concrete need. Run linter, formatter and type check before calling a diff ready, and say plainly that they do not prove runtime behavior. External automation and publishing APIs are covered below. Studio-side workflow with the official MCP server is in [Studio MCP](studio-mcp.md).

## Open Cloud and external automation


- **What it is:** REST APIs for managing Roblox resources from outside the game: update or publish games, restart servers, work with data stores and memory stores, manage user restrictions, list inventory items, automate in CI.
- **Authentication:** API keys are the easiest start; OAuth 2.0 suits apps that act for other users. Prefer endpoints that support either (stronger stability guarantees). Legacy cookie-authenticated APIs can change without notice and are not recommended for production.
- **Webhooks** notify your service about events such as refunds or subscription changes. Treat every webhook as untrusted input: verify, deduplicate, respond quickly.
- **From inside a game:** `HttpService` can call a subset of Open Cloud endpoints. Never put an API key in a script that clients can read, and never in replicated containers; use the Secrets store (`HttpService:GetSecret`, verify in the docs) or an external service.
- **Least privilege:** one key per purpose with only the scopes it needs, restricted to the required universe, with a plan for rotation and revocation.
- **Safety:** an automation can publish or overwrite live data. Dry-run first, log every call, and get the owner's approval before any write against a live universe ([release checklist](release-checklist.md)).
- **Good uses:** CI that publishes a *test* place, scheduled data export, ban sync, restart after a hotfix. Combine with [tooling](tooling.md) (Rojo, Wally, linters).

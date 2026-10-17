# Architecture conventions: feature folders, public APIs, script layout

An optional, opinionated way to organize a Roblox codebase around **features that own their own files and expose one public surface**. Use it for new systems and for scripts you write or substantially edit. If the project already follows another convention, keep that convention for existing code and mention the mismatch; a small fix never justifies reorganizing everything. Written for this plugin; the general idea of feature-owned folders and API modules is common practice in the Roblox community.

## The idea in one paragraph

Every feature gets a home in each container that needs it. Everything a feature owns lives there, and other features reach it only through a single API module. Then two questions are always answerable: "what can this script touch?" (its own folder plus other features' APIs) and "what breaks if I change this feature?" (only the API's callers).

## Folder map

| Location | Contents |
| --- | --- |
| `ServerScriptService/<Feature>` | Server scripts, modules and the server API |
| `StarterPlayer/StarterPlayerScripts/<Feature>` (or `StarterCharacterScripts`) | Client scripts and modules |
| `ReplicatedStorage/<Feature>` | Modules both sides use, including a shared or client API |
| `ReplicatedStorage/Assets/<Feature>` | Assets clients need (UI, models, sounds) |
| `ServerStorage/<Feature>` | Assets only the server needs |
| `Workspace/Scripted/<Feature>` | World objects the feature drives; prefer CollectionService tags over fixed paths |
| `ReplicatedStorage/Libraries`, `ReplicatedStorage/Packages` | Generic utilities, package-manager output |

Search the Explorer for a name before creating a feature, and avoid names other features might want (`Sounds`, `UI`, `Data`). Tools cannot live in feature folders inside `StarterPack`, so keep the tool in its feature folder and parent it to `StarterPack` at runtime; keep the tool's UI inside the tool, name it `<toolName>Tool`, and show or hide it explicitly in code rather than depending on `ResetOnSpawn`.

## Public surface: API modules

- A feature's internals (attributes, values, remotes, folder contents) are private. Other features call its API module instead of reading `player.leaderstats.Coins.Value` or flipping a `Ragdolled` attribute directly. That lets the owner change the implementation without touching callers.
- Name the API by where it can run:
  - `<Feature>API` - server only, inside the feature's `ServerScriptService` folder.
  - `<Feature>ClientAPI` - client only, in the feature's client module folder.
  - `<Feature>SharedAPI` - usable by both, in `ReplicatedStorage`.
- Expose functions and event signals with clear argument types instead of loose BindableEvents that callers must discover by reading internals.
- Inside one feature, scripts may talk through remotes and events freely; the API line only separates public from private.
- Wrap frequently used engine calls that you will probably want to observe later (for example applying damage in a combat game) in a feature with an API, so tracking or rules can be added in one place.

## Dependency direction

Aim for "removing a feature edits nothing outside it". When Audio should react to Weather and Zone changes, **Audio subscribes** to their events; Weather and Zone do not call Audio. Dependencies point at the stable, general feature, never from it to its consumers.

## Sub-features

- A sub-feature is a folder inside its parent feature (for example `Abilities/Fireball` inside `Ability`) used only by that parent; other features never reach it.
- If all sub-features follow one automatable pattern (each ability module exposes the same `activate` function), the parent can load them directly and they need no API. Without such a pattern, give each an API.
- Only the direct parent talks to a sub-feature; a grandparent goes through the parent.
- Shared rules (cooldowns, can-activate checks) live in the parent so a rule change happens once.

## Script template

Order the top of a script so dependencies are visible at a glance:

1. Services (`game:GetService`)
2. Other features' APIs (variable name = module name)
3. The feature's own modules
4. The feature's remotes and events
5. Asset references (GUIs, models, anything outside the script's own folder). Keep `script.Parent`, `ReplicatedStorage.X` style lookups here and nowhere else in the file.
6. Constants
7. State variables
8. Local functions
9. The module table, then its functions (modules only)
10. Connections (`PlayerAdded`, remote handlers)
11. `return` (modules only)

## Naming

- Spell names out (`player`, `humanoidRootPart`), no abbreviations.
- camelCase for variables, functions and methods; PascalCase for required modules, APIs, services and classes.
- Add a type suffix to remote and event variables: `purchaseRE` (RemoteEvent), `fetchDataRF` (RemoteFunction), `roundEndedBE` (BindableEvent), `getStateBF` (BindableFunction).
- Name modules so the running side is obvious: `Inventory`, `InventoryClient`, `InventoryShared`.
- Use precise names: `cooldownEndedBE`, not `cooldownBE`.
- A script's name must describe everything it does. A script that handles visuals and hitboxes is `Fireball`, not `FireballVisuals`.

## Hygiene

- Use `--!strict` and type annotations for new modules.
- Comment the *why* (a workaround, a constraint, what breaks otherwise), not what the code already says.
- Remove commented-out code, leftover debug prints and unused assets (or move them to a `Trash` folder pending approval).
- On the client, wait for runtime-created or late-replicating instances with `WaitForChild` and a timeout, and handle the "not available" case (PlayerGui contents, early ReplicatedStorage content, streamed Workspace content). On the server, index directly for things you created or that exist at start. With StreamingEnabled even `WaitForChild` cannot guarantee a Workspace instance.
- Keep functions short, loops bounded, control flow plain, and check return values.

## Restructuring an existing project

1. Back up scripts first (the project may not be in version control).
2. Audit read-only: proposed features and sub-features, cross-feature accesses and the API that replaces each, dependency-direction violations, dead assets, name collisions. Save it as `RESTRUCTURE_AUDIT.md` (confirm the location; never overwrite) and wait for the owner's approval.
3. Migrate one feature at a time: create folders, move files, add the API, update callers, fix every `require` path, run one sanity check, continue.
4. Clean up dead code, prints and unused assets.
5. No behavior changes. Keep DataStore keys, schemas, attribute names used by saved data and product IDs unless the owner approves a change.

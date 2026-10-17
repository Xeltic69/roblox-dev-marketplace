# Durable state, session ownership and recovery

Classify data as session-local, durable profile, temporary cross-server coordination or notification. Use stable keys/IDs, plain serializable fields and explicit schema versions. Keep fields together when a transition needs one durable record. Integrate with the existing data owner; never add a second writer beneath a profile library.

## Load and migrate

Distinguish successful missing data from a failed read. A failed load must not create defaults that later overwrite unknown real progress. Disable valuable mutations or use a clearly marked read-only/failure state until recovery. Deterministic migrations handle old schemas, repeat attempts and unknown newer schemas. Filling missing defaults is not a semantic migration. Test migration compatibility with the rollback/release plan.

Consult [DataStores](https://create.roblox.com/docs/cloud-services/data-stores), [versioning/caching](https://create.roblox.com/docs/cloud-services/data-stores/versioning-listing-and-caching), and live [limits/errors](https://create.roblox.com/docs/cloud-services/data-stores/error-codes-and-limits). Do not freeze old size limits, shutdown-time folklore, or fixed quota tables into production rules; read the live limits page.

## Single-record commit

UpdateAsync offers a single-key read/modify/write, not a database-wide transaction. Its non-yielding transform can rerun; keep it free of external effects such as granting Tools, changing leaderstats, sending remotes or calling another service. A stale full snapshot can still overwrite newer state if the transform ignores the current record. Preserve relevant metadata/user associations properly. See [GlobalDataStore](https://create.roblox.com/docs/reference/engine/classes/GlobalDataStore).

Use a stable operation identity to make retries converge. After success, update runtime presentation from accepted state. A failed response can have an unknown commit outcome; reconcile through the data layer or an appropriate uncached read before compensation. Do not label a retry or local refund atomic merely because it uses UpdateAsync somewhere.

## Session and save lifecycle

If profiles may be opened by multiple servers, establish session ownership atomically and positively verify it on writes. Refresh leases, release after the final save and stop valuable writes if ownership is lost. Serialize saves/retries per owner so an older request cannot overwrite a newer state. A maintained profile library may provide this; verify its current contract instead of mandating a dependency or mechanically renaming old ProfileService methods.

Stagger saves and bounded backoff/jitter. Save periodically and at relevant lifecycle points, including leaving/shutdown. Track completion/deadline instead of waiting an arbitrary five seconds and assuming success. Shutdown has a bounded opportunity; it is not a guarantee for every pending write. See [best practices](https://create.roblox.com/docs/cloud-services/data-stores/best-practices) and [player data/purchasing](https://create.roblox.com/docs/cloud-services/data-stores/player-data-purchasing).

## Temporary coordination

MemoryStore is an expiring service across servers, not one server's local table. Choose TTLs, claim/invisibility behavior, renewal and recovery. A server shutdown does not imply all service entries disappear. Queue claims can reappear; workers need idempotence. Messaging notifies, while storage remains authoritative; consumers must tolerate missed/stale/repeated signals. See [MemoryStore](https://create.roblox.com/docs/cloud-services/memory-stores) and [cross-server messaging](https://create.roblox.com/docs/cloud-services/cross-server-messaging).

## Verify in isolation

Use separate test data/universe for real service tests. Exercise failed load, absent profile, throttling, stale save retry, concurrent ownership, lost lease, shutdown, migration repeat, unknown commit and reload. Mocks prove your contract handling, not actual platform durability. See [monetization](monetization.md) and [transactions](economy-transactions.md) for related irreversible operations.

## Leaderboards and cross-server extras (verify limits in the docs)

`OrderedDataStore` fits leaderboards: it stores integer values and returns sorted pages, but it does not replace the profile data and lacks some standard data store features; read the current [data store docs](https://create.roblox.com/docs/cloud-services/data-stores) for supported methods, limits and versioning before relying on it. Write leaderboard entries from the owning system API after the authoritative save, throttle updates, and treat a leaderboard as eventually consistent. For cross-server events use MemoryStore or MessagingService as described above, with idempotent consumers.

## Shutdown saves (BindToClose)

Register `game:BindToClose` once per server to save every player still in the game when the server shuts down. The server waits up to 30 seconds for all bound functions to finish and then shuts down regardless (a ceiling, not a guarantee), so start all saves in parallel, track completion, and finish before the budget ends; do not do slow work first. In Studio, avoid writing test data to production stores in this callback (the official sample returns early with `RunService:IsStudio()`). Keep this path idempotent with the normal leave save so a double save cannot corrupt or roll back data.

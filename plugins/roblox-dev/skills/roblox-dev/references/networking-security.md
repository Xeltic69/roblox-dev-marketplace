# Multiplayer contracts and security boundaries

Document each action's direction, payload, allowed sender, authority, response, frequency, deduplication scope and state preconditions. The Player provided by Roblox identifies the sender; a claimed target user ID needs authorization. Resolve prices, ownership, rewards and legal destinations from server data.

## Validate and bound

Validate types, shape, list length/depth, finite values, allowed IDs, instance ancestry/class, alive state, ownership, distance, resources and cooldown before expensive work. Reject duplicate identities in one valuable operation. Presentation eligibility is helpful UX, not authorization. Touch, prompt, click and client-owned physics events also need contextual validation. See [client/server boundary](https://create.roblox.com/docs/scripting/security/client-server-boundary).

Use rate limiting and processing budgets appropriate to action cost and normal gameplay. A client debounce alone cannot protect the server. Rate limiting does not serialize an operation; explicitly lock/queue conflicting mutations, then revalidate after yielding. Do not assume OnServerEvent callbacks become a transaction queue when a handler yields.

## Message semantics

Reliable events suit consequential transitions; RemoteFunctions yield callers and need failure handling. Avoid server-critical InvokeClient flows controlled by an unreliable client. Slow operations benefit from request identity, an asynchronous outcome and authoritative reconciliation. Unreliable streams are suitable only for loss/reordering-tolerant presentation/latest-state data, not purchases or reward counters. Read [remote communication](https://create.roblox.com/docs/scripting/events/remote).

Use snapshots plus revisioned incremental updates for late join and resynchronization. Detect stale updates and gaps. Do not assume a remote guarantees that all related instances/properties are already present, especially under streaming. Preserve private state; do not broadcast full inventories or blindly relay raw client payloads.

Specify action cardinality: one reward claim per period, repeatable attack within cooldown, one item consumption, one completion per round ID, or a repeatable purchase tied to a distinct real receipt. A client-generated request ID is a correlation/deduplication aid, not entitlement to an operation.

## Prediction and physics

Predict reversible cosmetics/input response where latency matters, then reconcile accepted state. Valuable ownership remains server-controlled. Competitive checks must consider legitimate teleports, vehicles, knockback, packet bursts and gameplay context; a single displacement threshold is not a universal ban rule.

If adopting engine rollback/server-authority simulation, verify current support, settings and compatibility in [server-authority documentation](https://create.roblox.com/docs/projects/server-authority). Simulation may rerun: use the documented simulation clock and keep irreversible awards, audio and particles outside rerunnable logic. Do not assume enabling a mode supplies the game's hit policy or durable transaction design.

## Verify

Test two distinct client observers for shared behavior and confirm server state, not just local animations. Include malformed/oversized payloads, spam, stale revisions, duplicate requests, delayed/reordered messages, leave/respawn mid-action and unauthorized ownership. Report which cases were actually executed. Scope defensive work to the feature unless a broader audit is requested.

## Text filtering and chat

Any text one player writes and another can see (names, signs, pet names, messages, drawings) must be filtered on the **server** for each recipient before display, with `TextService:FilterStringAsync` (and the result methods for chat or non-chat display) or the built-in chat system (`TextChatService`). Never broadcast the raw string, and handle filtering failure by not showing the text instead of falling back to the original. Persisted text is filtered again when it is rebroadcast. Verify the current API names in the [text filtering docs](https://create.roblox.com/docs/ui/text-filtering).

## Remote variants

- `UnreliableRemoteEvent`: for frequent, non-critical data that may be dropped or arrive out of order (cosmetic updates). Messages with a payload above about 1,000 bytes may be dropped, and ordering is not guaranteed, so include a sequence number or timestamp and ignore stale messages. Never use it for purchases, damage or state that must arrive.
- `RemoteFunction`: never call `InvokeClient`; a client can error or never return and hang the thread. Treat every client return value as untrusted.

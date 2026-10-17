# Luau, modules and state ownership

Use idiomatic Luau and the project's analysis/style conventions. Strict mode and explicit exported contracts are useful for new maintained modules, but a targeted fix does not require annotating untouched files. Distinguish static typing from runtime validation at untrusted boundaries. Use tagged states to expose lifecycle, rather than optional fields whose relationship is implicit. See [Luau types](https://luau.org/types/) and [syntax](https://luau.org/syntax/).

Illustrative contract, not a runtime module:

```luau
--!strict
export type LoadState<T> =
    { status: "loading", generation: number }
    | { status: "ready", generation: number, value: T }
    | { status: "failed", generation: number, message: string }
```

Refine unknown values rather than hiding invalid assumptions under broad any casts. Guard sparse-array length assumptions, unordered dictionary traversal, and mutable shared tables. An explicit dependency sequence is necessary when initialization order matters; task.spawn over a dictionary is not ordered startup.

## Runtime placement and modules

Keep private server logic/templates in server containers and public/shared contracts in replicated containers. ReplicatedStorage contents are visible to clients; hiding a UI control does not hide a secret. A ModuleScript's state is local to its execution environment, not a shared object spanning client and server. Inspect [DataModel guidance](https://create.roblox.com/docs/projects/data-model) and current script run-context rules before moving scripts.

Separate synchronous construction from starting listeners/yielding work when useful. Avoid require cycles and indefinite module-startup waits. Expose a small meaningful interface; do not introduce a framework only to gain Init/Start labels. Existing React/Fusion/Vide, service frameworks or ECS should retain their ownership conventions unless a migration is requested.

## Ownership and async work

Assign a single mutation owner to each authoritative field. Other systems request transitions and subscribe to snapshots/events. Define readiness and failure as state, not a guessed sleep. Before and after yielding, check the active player/session/character/view generation and current prerequisites.

Separate scopes: game lifetime, player lifetime, character lifetime, round, screen and streamed target. Each scope owns subscriptions, timers, tasks, tracks and instances. Cleanup is idempotent and prevents delayed work from reviving obsolete state. Reconcile already-existing objects with newly observed lifecycle events without attaching twice. Useful illustrative guard:

```luau
local generation = 0
local function invalidatePendingWork()
    generation += 1
end
local function stillCurrent(captured: number): boolean
    return captured == generation
end
-- After any yield, also verify the owning session/target still exists.
```

The guard does not cancel a committed server operation or create a transaction lock. Use explicit serialized queues/locks for state mutations whose callbacks can overlap through yields. Keep cleanup and domain authority separate.

## Editing existing code

Read callers and data owners, identify the exact trigger, then patch the smallest complete path. Preserve public APIs or update their callers coherently. Do not edit generated output; understand the source tool first. For a refactor, define behavior equivalence and recovery, then prove relevant regressions. Do not rename/restructure unrelated modules to match a skill's preferred architecture.

## Deprecated or discouraged APIs (verify in the API reference)

| Avoid | Prefer |
| --- | --- |
| `wait()`, `spawn()`, `delay()` | `task.wait`, `task.spawn` / `task.defer`, `task.delay` |
| `RunService.RenderStepped` for new code | `PreRender` / `BindToRenderStep` (client only) |
| `Model:SetPrimaryPartCFrame` | `Model:PivotTo` |
| `Humanoid:LoadAnimation` | `Animator:LoadAnimation` |
| `BodyVelocity`-style body movers | Mover constraints |
| Raw `SetAsync` on shared player data | `UpdateAsync` with session ownership, or a vetted profile library |

Wrap fallible service calls (DataStore, Marketplace, HTTP) in `pcall` with bounded retry and backoff, and never swallow an error silently.

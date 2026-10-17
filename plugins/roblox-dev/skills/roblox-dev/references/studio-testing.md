# Studio inspection, debugging and test evidence

Discover the actual exposed tools, correct Studio instance and initial play state. Prefer purpose-built script/instance inspection and exact edits. Select Edit versus Server versus Client according to the task; do not execute arbitrary modules merely to inspect them. Some connectors require studio_id for every call and have different capabilities; current schema wins over old tutorials. When a connection is already configured, routine setup is outside scope. If none is available, use the offline route rather than assuming access.

## Work safely in the intended source

Identify whether Studio, filesystem sync or generated output owns each surface. Persist intended changes in edit-time/source files, not only disposable runtime objects. Use bounded batches, readback and scoped roots for construction. Re-running should not create duplicate scripts, screens or listeners. Preserve unrelated user work, current debugger breakpoints and active sessions.

Start/stop only as needed and authorized for the current task. A user already playing does not imply permission to clear all runtime/debugger state. Record and restore task-owned device/camera/test modifications. When testing guidance or scripts that are not part of the task, use an isolated workspace and leave the open game untouched.

## Debug loop

Reproduce → inspect involved code/callers → identify authority/state → observe values/events → test one hypothesis → patch → rerun. Prefer a meaningful state transition over adding delays. Capture request/round/generation/revision identity when relevant; avoid secrets or unnecessary raw user content.

If the Studio connection exposes Roblox-authored debugging guidance, fetch it for runtime breakpoints/logpoints. Debugger data can become invalid after resuming; do not keep stale frame handles as evidence. Preserve the user's breakpoints and remove only added instrumentation. A failed reproduction warrants better evidence, not progressively wider speculative edits.

## Test layers

| Layer | Proves | Does not prove |
| --- | --- | --- |
| Source/types | Syntax/contracts and inspected logic | Actual platform flow or appearance |
| Isolated fixtures | Deterministic transitions/error handling | Live service delivery/durability |
| Solo Play client/server | The observed local player path | Two distinct clients or network scale |
| Multi-client | Shared authority/replication in tested cases | Every latency/population scenario |
| Screenshots | Visible state at that moment/view | Click behavior, hidden state or hardware performance |
| Device/controller emulation | Layout/input conditions tested | Real-device frame cost/thermal limits |
| Published isolated service test | Tested external behavior | Production data safety without isolation |

Follow [Studio testing modes](https://create.roblox.com/docs/studio/testing-modes). If a play-control tool lacks client-count orchestration, do not claim multi-client coverage from one Play call. A server harness cannot certify client-only UI. Teleports and published analytics need their actual supported environment.

## Choose meaningful checks

UI: actual PlayerGui, representative content, flow, focus, reopen/respawn, late response and narrow layout; use [UI verification](ui/verification.md). Multiplayer: late join, shared/private state, simultaneous actions and disconnect. Persistence/paid grants: duplicate operation, interrupted commit, saved reload and isolated failures. Rounds: full cycle twice, late join/death/tie/stale event. Performance: matched baseline/workload and actual available target device.

Use the project's existing tests (Jest Lua preferred for new work; TestEZ only if already used; or custom) when appropriate; do not migrate frameworks or edit engine flags by default. Inject clock/storage/services for pure state tests where useful. Fetch Roblox-authored unit-test guidance if exposed; unit tests do not replace gameplay QA. Framework/version environments need current docs: [Jest Lua](https://github.com/jsdotlua/jest-lua), [TestEZ](https://roblox.github.io/testez/).

Cloud or real service tests require dedicated test data/universe and scoped credentials; research does not authorize publication or service writes. Tool/schema inspection is read-only evidence about capability, not evidence a game recipe ran.

## Offline

Continue implementation, static checks and pure fixtures when Studio is unavailable. Deliver source with placement, initialization, expected flows and a concise pending runtime-check list. Do not fabricate screenshots, clean console output or successful integration. Distinguish missing tool capability from a defect in the code.

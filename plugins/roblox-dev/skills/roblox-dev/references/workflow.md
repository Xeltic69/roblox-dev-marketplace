# From request to integrated game

## Improve an existing game

Establish a baseline of the requested experience: player path, triggering defect, affected services, data ownership, and existing framework. Search narrow symbols/paths before reading the whole project. Identify generated files and sync ownership so Studio edits do not fight a filesystem tool. Record unrelated existing errors separately.

For a specific defect, trace where observed state first diverges from expected state. Reproduce before applying an architectural fix. For broader improvement, rank findings by player impact, evidence, cost, and dependencies. Implement connected changes the task requires, not a catalogue of every possible optimization.

Keep a short acceptance ledger for longer work: requirement, implementation location, evidence, status, remaining gap. Updating a plan does not establish completion. A successful bootstrap does not prove purchases, respawns, or mobile input work.

## Build a new game

Define fantasy, primary action, goal, feedback, risk/reward, session shape, replay reason, supported inputs, and content scope. Use [game-design.md](game-design.md) and the relevant technical routes. Infer routine details; do not require redundant genre confirmation or a fixed MVP/full-vision menu when the user's scope is already clear.

Prioritize the riskiest assumption: whether the mechanic is understandable/fun, whether interaction works across clients, or whether critical assets/integration are available. Prototype that assumption inside the intended scope. Then develop complete slices: entering → learning → acting → resolving → progressing/restarting. Prototyping is a phase, not permission to stop before the requested final game exists.

A vertical slice should connect its world, state, controls, feedback, success/failure, and replay. Add persistence or monetization only when the game and request require them. Build content progressively and validate representative complexity before multiplying assets or levels. Adopt frameworks only for a demonstrated need or existing project choice.

## Integration and recovery

Map each subsystem's inputs, outputs, authority, startup dependency, state ownership, and shutdown cleanup. Specify timing for data ready, character ready, round ready, and screen ready rather than scattering indefinite waits. Use explicit failure states for missing services/assets. Test joined-late players against an initial snapshot, not only events emitted before they joined.

For consequential refactors, preserve a recoverable local baseline and stage changes so evidence remains attributable. Avoid replacing the entire place hierarchy, clearing all breakpoints, disabling unrelated controls, or deleting the user's work to make an example run. Track created roots and instrumentation; cleanup removes those only.

## Review-only outcomes

Return prioritized, actionable findings with trigger, affected location, consequence, and suggested correction. Separate observed defects, probable risks, and design opinions. Do not fabricate profiler measurements or exploit reproduction. If the user authorizes fixes, carry relevant implementation through verification rather than stopping at the findings list.

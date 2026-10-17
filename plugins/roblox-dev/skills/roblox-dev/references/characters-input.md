# Characters, movement, camera, and input

Inspect rig/controller, character lifecycle, camera ownership, input bindings, and current physics authority first. Standard controls may already meet the request. Custom characters, movement modes, or beta simulation features need current documentation and project opt-in; do not replace them as a prerequisite for a small change.

## Lifecycle

Bind player-level state once and character-level state per character generation. Handle an existing character as well as future character-added/removal events. Release old Humanoid, Animator, tool, effect, and input subscriptions. Delayed work captures the generation and checks that it still owns the active character after yielding. Missing or streamed targets need a bounded wait, retry, or explicit unavailable state rather than indefinite assumptions.

Keep durable inventory/progression separate from character instances. Restore equipped visuals from canonical ownership under the game's respawn rules. Respawn occurring during an ability, purchase, cutscene, or round should not duplicate grants or leave controls frozen. Verify current [Player](https://create.roblox.com/docs/reference/engine/classes/Player) respawn APIs before custom spawning.

## Movement and camera

Use impulses for a discrete push and supported constraints/controller mechanisms for sustained movement. Guard zero and non-finite vectors before normalization. Time integration uses measured delta or the explicit timestep of an opted-in simulation system; task.wait duration is not a guaranteed timestep. Movement authority affects hit validation and rewards; see [networking-security.md](networking-security.md).

Camera is per-client presentation. Define which system owns it during gameplay, dialogue, cutscenes and spectating. Restore camera mode/subject/FOV, cursor state and render callbacks when a flow completes, skips, dies or loses its target. Test obstructed views, zoom extremes and rapid mode switching. Camera shake must not remove gameplay readability and should offer an appropriate reduced-motion alternative. See [camera guidance](https://create.roblox.com/docs/workspace/camera).

## Input contract

Represent actions independently of keys: open inventory, select, cancel, equip, jump, interact. All supported devices should have a path to the action, but not necessarily identical gestures. Preserve existing input architecture. For new contexts, consult the [Input Action System](https://create.roblox.com/docs/input/input-action-system); coexistence with old bindings must avoid double-firing. Menu and gameplay contexts need priorities, restoration and explicit ownership.

Respect input already processed by UI/core systems and text editing; raw listeners must not trigger abilities while the player types. Active input can change at runtime; [PreferredInput](https://create.roblox.com/docs/reference/engine/classes/UserInputService) is more informative than treating TouchEnabled as the current control scheme. Do not override platform-reserved input or globally disable core controls for a nonblocking panel.

Map selection, submit/cancel, drag, slider steps and hold actions through the same accepted-action path. Track the initiating touch/pointer during dragging, including release outside the control. Gamepad selection needs a reachable graph, a sensible initial target and focus recovery after a target is removed. Use [UI component contracts](ui/components.md) for native button behavior and focus.

## Check

Join with existing character, respawn repeatedly, leave during a yielding operation, swap devices, type with gameplay hotkeys active, open/close blocking menus, and interrupt camera modes. A desktop mouse test does not establish console or touch support. For animations, use [presentation-assets.md](presentation-assets.md).

## Names worth knowing (verify in the docs)

Camera: `workspace.CurrentCamera`, `CameraType` (use `Scriptable` only while your controller owns the camera, restore afterwards), `CameraSubject`, and `RunService:BindToRenderStep` at a camera-appropriate priority. Input: `ContextActionService:BindAction` for rebindable actions across keyboard, gamepad and touch; in `UserInputService` handlers always check `gameProcessedEvent` so typing or UI input does not trigger gameplay.

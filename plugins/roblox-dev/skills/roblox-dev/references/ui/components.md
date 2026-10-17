# Roblox component contracts

Generate only what the requested screens need. Components share semantic tokens and behavior contracts while allowing any reference-driven appearance. The following are specifications, not supplied or tested runtime modules.

## Shared contract

A reusable component accepts content, layout constraints, relevant state, optional style overrides, and callbacks expressing user intent. Return or expose a root instance, a way to update its state, and cleanup when the project architecture needs them. Choose names consistent with the project. Keep enabled, selected, focused, loading, locked, and completed meanings distinct.

Use one state resolution policy: unavailable/loading states must gate activation; selected and focus indicators can coexist; pointer hover is optional. Do not rely on appearance alone to block actions. Centralize competing feedback animations. Use `GuiButton.Activated` for ordinary cross-input activation rather than a mouse-only event. See [GuiButton documentation](https://create.roblox.com/docs/reference/engine/classes/GuiButton).

## Control recipes

| Component | Content/state contract | Behavioral requirements |
| --- | --- | --- |
| Button/icon button | Label or recognizable icon, role, enabled, loading, callback | Prevent repeated activation while pending; retain an understandable label; communicate icon-only meaning where needed |
| Toggle | Label, boolean value, enabled, change callback | Controlled value follows the owning state; show both on and off meaning without color alone |
| Slider | Label, current value, min/max/step, formatting, change/commit callbacks | Clamp and quantize values; separate live feedback from committed changes; support non-pointer adjustment when in scope |
| Dropdown | Options with stable IDs, selected ID, enabled, change callback | Keep selection stable during updates; bound popup size, scroll long options, handle dismissal and focus return |
| Text/search input | Label, value, placeholder, validation/pending state, change/submit callbacks | Distinguish placeholder from label; preserve editing and focus; do not steal gameplay hotkeys while typing |
| Tabs | Stable page IDs, labels, selected ID, callback | Keep tab selection and page state synchronized; choose a fallback if the selected page disappears |
| Progress/cooldown | Value and maximum or start/end times, label, semantic role | Handle zero maximum and out-of-range values; display meaningful completion/unavailable state; stop updates when idle |
| Item card | Stable item ID, asset, name, quantity, availability, selected state | Separate inspect, equip, and purchase intent; remain legible without an image; update by key |
| List/grid | Items, key function, ordering/filter, render recipe, selection | Show empty/error/loading states; preserve selection by key and scroll when reasonable |
| Dialog | Title, message, named actions, dismissal policy | Explicit result for confirm/cancel; one resolution only; support stacking only when needed |
| Tooltip | Anchor, short content, visibility triggers | Remain within bounds; avoid intercepting activation; offer focus or tap access when important |
| Notification | Message, semantic role, duration or persistence, optional action | Bound queue length, handle replacement/stacking, expose important errors beyond a fleeting toast |

These are behavioral contracts, not instructions to assign identical shapes, sizes, or colors. A locked item can explain how to unlock it without activating its unavailable gameplay action.

## Layout and input details

Prefer content-driven containers for repeated content and anchored placement for HUD composition. Combine proportional size, fixed spacing, measured text, and constraints intentionally. Neither all-scale nor all-offset sizing works universally. Avoid circular size dependencies between automatically sized parents and proportionally sized children.

Decide whether a control emits updates continuously or only on commit. For pointer drag, track the initiating pointer/touch and handle release outside the control. Respect scrolling versus dragging intent. Map keyboard/gamepad steps to the same value-change path instead of creating different logic for each device. Use available native drag mechanisms when appropriate and verify their current API before adopting them.

Support long labels and platform text preferences where feasible. Do not reduce text until it fits an arbitrarily small box. Expand, wrap, truncate with a detail path, or change composition according to content importance. Focus indicators must remain visible over the chosen material and background.

## Item and character previews

Use a ViewportFrame when an actual model preview is requested. Isolate the preview model, provide its own camera, and frame from bounds so different items remain visible. Choose consistent lighting, orientation, and padding. Reframe when the model changes; avoid coupling the preview to the gameplay camera. Use an appropriate preview world when animation requires it and verify platform behavior.

Inspect inserted models and avoid executing embedded scripts as part of a visual preview. Provide a loading/fallback image if content is unavailable. Limit simultaneous expensive or animated previews and clean them up when removed. Do not assume every inventory cell needs a live 3D preview.

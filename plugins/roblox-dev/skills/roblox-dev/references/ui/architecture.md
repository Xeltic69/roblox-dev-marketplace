# Roblox architecture and screen management

## Project discovery and delivery

Inspect the intended Studio project or local source tree, existing UI framework, theme, controllers, and data interfaces. Confirm the target project from available context rather than mutating whichever Studio connection appears first. Use available Studio tools when connected; otherwise provide editable Luau files with explicit placement and setup. Detect capabilities from the tools actually exposed, not a presumed server version or fixed tool count.

Choose a delivery appropriate to the project: editable GUI instances with client controllers, a component-based construction system, or modules in the established framework. Preserve the existing approach unless changing it is part of the request. Avoid runtime-only construction when the user asks for a screen editable in Studio. A preview screenshot alone is insufficient for an implementation request.

Make construction safe to rerun: identify the root owned by the task, update or replace only that root, and avoid duplicate controllers or listeners. Inspect before removing anything. Preserve unrelated ScreenGuis and CoreGui behavior. Keep demonstration fixtures separate from production bindings.

## Responsibilities

Separate these responsibilities conceptually; small screens may combine them without requiring one module per row:

| Responsibility | Owns |
| --- | --- |
| Theme | Semantic colors, type roles, geometry, spacing, motion, asset references |
| Components | Reusable visuals and local input behavior |
| Screen/view | Composition and rendering of a supplied state |
| Controller | Navigation, user intent, async request state, lifecycle |
| Data adapter | Existing game snapshots, subscriptions, and action requests |
| Bootstrap | One-time mounting and explicit cleanup |

Keep game services and remote calls out of generic button or card builders. Reuse the project's state and cleanup libraries when present. Prefer an ordinary theme table for a small isolated build; use the project's styling mechanism when already established. Do not add framework dependencies as a prerequisite for a simple screen.

## State and navigation

Define the relevant screen states and transitions before wiring actions. For example: closed → opening → open → closing → closed. Define request state separately so closing a panel does not imply a request failed or succeeded. Handle rapid open/close actions deterministically: cancel competing transitions and converge to the newest intended state.

For multi-screen tasks, specify whether navigation replaces a page, pushes a detail view, switches a tab, or opens a modal. Maintain a back path and restore selection where useful. Model a modal stack only when nesting is needed. Only the top blocking modal should receive background interactions; decide whether dismissal by backdrop, back key, or close button is appropriate to that modal. Do not let backdrop dismissal silently confirm an action.

Record prior focus when opening an overlay. Move focus to a sensible active control when needed, then restore it on close if the original control still exists. Resolve focus when a selected element is filtered out or destroyed. Gameplay bindings that conflict with a blocking UI should be coordinated through the existing input controller and restored on dismissal. Do not indiscriminately disable player controls for all menus.

Use deliberate layering for HUD, normal panels, notifications, and blocking overlays. Maintain a consistent relationship between ScreenGui ordering and descendants' layering. Do not solve overlap bugs by arbitrarily increasing every ZIndex.

## Lifecycle and performance

Decide whether each screen survives respawn or is rebuilt; preserve state intentionally. Bind character-dependent HUD data to the current character and release old subscriptions when the character changes. Mount once, clean up once, and make disposal safe if called again.

Each component/controller should own its connections, active animations, scheduled tasks, and temporary instances. Cleanup must prevent a delayed callback from touching a destroyed view. Hidden panels may keep lightweight state subscriptions, but pause expensive preview rendering or decorative updates. Prefer data-change-driven display updates to polling every frame.

For large lists, use stable item keys and update existing entries. Introduce pooling or virtualization when representative content shows excessive creation or layout cost; account for variable row heights, selection, and scroll position. Do not build complexity for a short static list.

Theme changes should update shared roles coherently without reconstructing the entire game UI. Keep animation transforms separate from responsive geometry. Avoid multiple systems writing the same layout property.

# Roblox interface patterns

Read only patterns relevant to the request. These define content and behavior, not visual presets. Combine them where useful and derive visual treatment from inspiration.

| Interface | Composition and state decisions |
| --- | --- |
| HUD | Rank health, resources, objective, and abilities by urgency; protect the gameplay viewing area; distinguish damage, depletion, cooldown, and unavailable actions |
| Inventory/equipment | Search/filter/sort where needed, stable selection, quantities, capacity, item detail and explicit equip actions; adapt detail panes on narrow layouts |
| Shop | Category browsing, accurate prices and ownership, item details, pending/cancelled/failed purchases; distinguish game currency from platform purchase flow |
| Settings | Group related options, display current values, define immediate versus apply/cancel behavior, handle defaults and saving failures |
| Dialogue | Speaker, readable text, advance/skip policy, choices, and history only if requested; allow full text reveal before advancing; handle changing choices |
| Quest/objective | Clear objective, progress, prerequisites and completion; distinguish completed from reward claimed; handle multiple tracked objectives without clutter |
| Skill tree | Prerequisites, cost, acquired/available/locked nodes, connections, inspect and unlock actions; make pan/zoom and a readable small-screen alternative deliberate |
| Rewards/progression | Explain eligibility, cost, reset effects, timing, and claimed states; confirm consequential resets when appropriate |
| Onboarding | Short steps tied to an actual task; back/skip policy, saved progress if needed, and an unobstructed path to gameplay |
| Leaderboard/social | Stable identity, ordering, ties and pagination where needed; differentiate loading from no entries; avoid hiding primary gameplay behind large tables |
| Main/pause navigation | Clear destination hierarchy, return to gameplay, current context, and predictable back behavior; decide which menus actually block gameplay |
| Notifications/dialogs | Persistent handling for important actionable errors, concise transient feedback, bounded stacking, and explicit confirmation results |

## Pattern-specific integration

Use server-provided timing/state for rewards and cooldowns when authoritative timing matters. Render remaining time from a suitable time basis and reconcile updates rather than sending requests every visual frame. UI timers do not grant eligibility.

For settings, classify preferences as local presentation or saved game/account state. Preserve the prior accepted value when saving fails, or keep an explicit unsaved draft. For equipment and skill unlocks, re-check displayed eligibility when new state arrives; the server remains authoritative.

For dialogue and player-authored text, distinguish trusted authored content from user input. Use the game's platform-compliant filtering path before displaying user-generated text to others. Do not treat a TextBox as permission to broadcast raw input.

## World interfaces

Use an on-screen container for overlays, a SurfaceGui for a physical display, or a BillboardGui for a camera-facing marker. For interactive surface or billboard controls, place the GUI under the player's GUI and associate the world target through Adornee; surface interaction also depends on the target part being queryable. See [Roblox world UI documentation](https://create.roblox.com/docs/ui/in-experience-containers).

Choose occlusion, distance visibility, lighting treatment, and apparent size for the gameplay purpose. A quest marker and a physical terminal have different visibility requirements. Rebind or remove the GUI if its target disappears, streams out, or is replaced. Do not leave interaction handlers pointing at a destroyed target.

World-space size units differ from ordinary on-screen proportions; inspect the target container's sizing rules before transferring screenshot dimensions. Test at representative distances and camera angles, not just from the editor's best view. Preserve readability without covering nearby characters or controls.

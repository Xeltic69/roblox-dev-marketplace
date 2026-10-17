# Roblox platform details

Read only the section for the requested platform. Verify unfamiliar or version-sensitive APIs against the current platform documentation when needed.

## Roblox Studio

For implementation structure and navigation, read [architecture.md](architecture.md). Use [verification.md](verification.md) to choose actual build checks. The main skill links the component, pattern, integration, and asset references by task.

Keep presentation client-side. Use reusable Luau components and a theme table; separate visual state from gameplay and server-authoritative actions. Connect existing systems where available. Client buttons must not independently grant purchases, currency, rewards, or progression. Identify any missing integration instead of showing invented success.

Inspect existing ScreenGuis and scripts before editing. Preserve relevant parenting, layering, and lifecycle behavior. Use layout containers, padding, size constraints, and scrolling to express composition. Give top-level windows a safe-area-aware fit strategy; adapt internal layouts when fit scaling would make text or controls too small. Do not carry over another game's baseline resolution, scale limits, or menu dimensions as universal values.

Treat viewport, orientation, and camera changes as layout inputs where relevant. Set up layout initially as well as on subsequent changes. Account for the selected ScreenGui inset behavior and avoid applying safe-area adjustments twice. Keep HUD elements clear of platform controls and core gameplay areas.

For proportion-sensitive icons, use an appropriate fit or aspect constraint. Do not constrain an entire flexible content region to a fixed aspect ratio merely because a screenshot has one. Prefer text hierarchy and measured containers to scaling every text label to fit. Handle long labels, larger counters, and more list items than the showcase contains.

Use buttons that support activation across input modes. Provide clear selected and gamepad focus states when those modes are in scope. Custom press and hover feedback should cancel or replace competing tweens and return to the correct state. If scaling a button, animate a stable visual child or wrapper; do not change its anchor without adjusting position. Disconnect callbacks and stop animations when the interface is removed.

Use native GUI elements for controls and text where practical. Generated artwork can supply illustrations or decoration, but a whole UI baked into an image cannot replace an editable, functional screen. Resolve assets through supplied files or available registries and test that they load in the experience; do not assume third-party IDs remain usable.

Inspect the result in Studio play mode if tools permit. Check a narrow viewport, a representative desktop viewport, menu opening and closing, long content, and relevant control states. Report any unavailable preview or integration precisely.

## Current API decisions

Read [ScreenGui](https://create.roblox.com/docs/reference/engine/classes/ScreenGui) for the relationship between ScreenInsets, clipping and inset compatibility. Separate a full-bleed decorative background from interactive content where the design needs both; do not assume IgnoreGuiInset alone solves every device safe area.

Use [list/flex layouts](https://create.roblox.com/docs/ui/list-flex-layouts) where their sizing and wrapping behavior fits content. Layouts can control child geometry; arbitrary writes to those same properties may be ineffective. Measure after layout resolves or respond to size changes, and avoid automatic-size cycles. Constraints solve specific bounds, not every overflow problem.

For device prompts, inspect [UserInputService.PreferredInput](https://create.roblox.com/docs/reference/engine/classes/UserInputService) and react when it changes. A touch-capable device may currently use a controller. Screen dimensions should guide layout while active input guides prompts and interaction. Consult [characters/input](../characters-input.md) before introducing a new input context.

Use the existing styling/framework choice. Roblox supports [shared styling](https://create.roblox.com/docs/ui/styling); adding it is optional. Fusion, Vide and React Lua have different state/lifecycle contracts; do not mix their ownership rules or migrate a working project to reproduce a reference. Follow the installed version's docs: [Fusion](https://elttob.uk/Fusion/0.3/), [Vide](https://centau.github.io/vide/), [React Lua](https://github.com/jsdotlua/react-lua).

For effects, current [appearance modifiers](https://create.roblox.com/docs/ui/appearance-modifiers) include native shadow and gradient options. Verify feature availability in the target engine before promising a particular effect. UIGradient applies to its parent, not the entire subtree. A shadow modifier on a text object represents its bounding area rather than automatically producing glyph shadows. Native shadows do not establish backdrop blur.

Respect relevant text-size, transparency and motion preferences using the current [GuiService](https://create.roblox.com/docs/reference/engine/classes/GuiService) contract where supported. Use localized live text, meaningful keys and layout expansion; inspect [localization guidance](https://create.roblox.com/docs/production/localization). Escape inserted user text when using rich text in addition to the game's filtering path. Fonts and fallback glyph coverage require actual verification.

## Localization

Use `LocalizationService` and translation tables with stable keys; `GuiBase2d.AutoLocalize` for static labels and `Translator:FormatByKey` for formatted strings in code. Read the player's locale from `Player.LocaleId`. Leave room for longer text in other languages, avoid text baked into images, and handle pluralization by key rather than string concatenation.

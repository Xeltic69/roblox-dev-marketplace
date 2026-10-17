# Roblox Studio workflow and verification

This is a textual build-and-check procedure. It does not itself execute Studio, supply a runtime library, or demonstrate that a generated interface works.

## Build with available capabilities

Inspect available tools and their current descriptions. Determine whether the environment can read instances/scripts, edit the intended project, run client play mode, inspect console output, capture screenshots, and simulate input or device sizes. Do not assume these capabilities travel together. A tool being listed is not proof that Studio is connected.

Use the smallest inspection needed to identify target UI roots, controllers, dependencies, and related data. Build within the existing project organization. Check whether edits apply to the saved/edit-time source or only to the live play session. Persist the intended source changes rather than delivering a temporary PlayerGui modification that disappears when play stops.

For offline work, provide the requested editable Luau source or textual implementation specification and exact placement/initialization steps. Mark Studio checks as unperformed. Do not claim screenshots or interaction evidence from code inspection.

## Practical check sequence

1. **Establish baseline:** inspect existing relevant UI and console issues before editing; note changes that the task owns.
2. **Build and open:** ensure the UI mounts in the intended client context and opens through the actual entry point. Check for duplicate roots, missing assets, initialization errors, and layering faults.
3. **Compare visually:** capture the visible client UI when possible. A screenshot of source code, a plugin widget, or an editor-only selection does not verify the player's screen. Compare major geometry and hierarchy before small decorative details.
4. **Exercise behavior:** follow the main task from start to finish; inspect relevant focus, pending, completed, disabled, and error states. Use controlled fixtures when the real service is unavailable and label that evidence as demonstration testing.
5. **Check adaptation:** inspect representative desktop and narrow mobile layouts, orientation where relevant, and gamepad navigation if in scope. Verify long content and maximum expected values rather than only attractive sample data.
6. **Check lifecycle:** repeat opening/closing, switch screens quickly, dismiss during a pending request, and respawn when relevant. Ensure callbacks, focus, animations, and character subscriptions recover correctly.
7. **Resolve observed faults:** fix the cause, repeat affected checks, and review the console again. Broaden testing only for a material remaining concern or an additional change.

If tool capabilities cannot expose the actual player's UI, retain the implementation, identify the precise missing check, and provide a concise manual check path. Do not stall indefinitely or treat an unavailable test as a pass.

## Choose checks by feature

| Feature | Useful additional cases |
| --- | --- |
| Dynamic inventory/list | Empty, one item, representative large collection, filtered-out selection, removed item, long names |
| Async action/purchase | Double activation, denied action, delayed response, close before response, uncertain outcome reconciliation |
| Navigation/dialog | Repeated opening, nested overlay if supported, back/dismiss, focus restoration, background input blocked appropriately |
| Slider/text input | Endpoint values, release outside control, non-pointer input, typing while gameplay bindings are active |
| HUD | Character replacement, zero/max values, rapid state changes, gameplay visibility, core-control overlap |
| Item preview | Unavailable model, unusually tall/wide model, model replacement, hidden-view cleanup |
| World UI | Near/far viewing, occlusion, angled view, target destruction or streaming changes, actual activation |
| Localization | Long translated labels, character coverage, number formatting, text wrapping and truncation |

Use focused automated checks when logic warrants them, such as request reconciliation or navigation state transitions. Avoid generating tests that merely mirror decorative constants. A visual skill also needs observed visual results; automated logic checks cannot establish appearance fidelity.

## Report evidence accurately

Deliver what was built, where it is editable, which reference traits were used, which flows/viewports were inspected, and remaining integration or test gaps. Distinguish edit-time screenshots from play-mode screenshots and device emulation from physical-device tests. Avoid blanket claims such as "universal," "fully optimized," or "works on all devices" based on a single showcase.

For platform behavior, consult current [Roblox UI documentation](https://create.roblox.com/docs/ui) and [ScreenGui documentation](https://create.roblox.com/docs/reference/engine/classes/ScreenGui), especially when adjusting safe areas, layering, or respawn behavior.

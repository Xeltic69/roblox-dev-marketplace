# Roblox data integration and assets

## Data adapter contract

Identify the game's existing source for each displayed value and action. Define a compact view state rather than passing an unrestricted service into every component. A useful adapter can supply an initial snapshot, subscribe to changes with a cleanup path, and request an action with a structured outcome. Follow existing project interfaces; these responsibilities do not prescribe a specific library or remote naming scheme.

Document fields that matter to the requested screen: stable item IDs, quantities, currencies, current settings, eligibility, selected equipment, and timestamps. Specify absent/unknown values instead of replacing them with misleading zero balances or success indicators. Keep demo values clearly separate and removable.

Use a request lifecycle such as idle → pending → accepted/rejected/failed, with the distinctions the task needs. Prevent accidental repeated submissions. Catch errors, show a recovery path, and keep unrelated UI responsive. Associate results with the request and view that issued them so an old response cannot overwrite a newer selection or reopen a closed screen.

Closing a screen does not cancel a server transaction. A UI timeout does not prove that a purchase failed. Reconcile uncertain outcomes from authoritative state before encouraging a repeat transaction. Use request identifiers/idempotency through the game's existing backend where duplicate granting is a concern. Do not invent success when a response or state update is missing.

Optimistic local feedback is appropriate for reversible presentation changes when reconciliation is defined. Do not optimistically grant items, currency, ownership, or progression. Gameplay requests should use the existing server validation for type, bounds, ownership, prerequisites, and request frequency. Keep this guidance scoped to the UI's integration rather than rewriting unrelated game systems.

A platform purchase prompt is a distinct flow from an in-game currency purchase. Opening or closing the prompt is not proof that a reward was granted. Reconcile ownership/grants through the game's established authoritative purchase handling. Verify current platform purchase APIs if adding that integration.

## Asset workflow

Keep a small manifest when multiple assets are involved: semantic name, provided file or verified asset reference, intended usage, crop/fit behavior, tint, and fallback. Use one compatible icon family and normalize optical weight and padding rather than merely giving all files identical dimensions.

Inspect supplied assets before using them. Determine whether images have baked text, margins, shadows, or backgrounds that would conflict with the chosen theme. Prefer live GUI text for localization and changing content. Use vector-like native geometry for simple borders and shapes; use raster artwork for illustrations or details that native geometry cannot reproduce well.

Prepare transparent cutouts, tileable textures, or scalable panel artwork only when needed. If generated artwork is requested, use the available image workflow and describe its role; do not generate a whole flattened UI to replace controls. Preserve source files and make uploads a traceable step. Upload only assets within the authorized task scope, and do not invent IDs or claim an upload finished before the tool confirms it.

Check that assets render in the intended experience and provide a deliberate fallback for unavailable content. Permissions, moderation, and loading can affect availability. Preload critical assets when appropriate without blocking the entire UI forever on optional images. Use sensible loading and failure states.

## Translating reference effects

Classify an effect before choosing implementation: native GUI property, layered native geometry, reusable image, 3D preview, or an approximation required by the engine. Examples include sliced artwork for scalable ornate frames, static texture for grain, and modest layered shadows when an exact reference shadow is unavailable.

Do not promise browser CSS effects, arbitrary font availability, or material behavior from a screenshot without verifying support. A translucent panel does not automatically blur content behind it. Approximate the important visual cue with readable contrast and explain a meaningful fidelity tradeoff. Avoid excessive layered instances for a minor effect, and inspect performance with representative content.

Use the user's existing styling system where available. Roblox also offers [universal styling](https://create.roblox.com/docs/ui) for shared appearance; verify its current workflow before introducing it into a project. An ordinary semantic theme remains a valid choice and does not require migration.

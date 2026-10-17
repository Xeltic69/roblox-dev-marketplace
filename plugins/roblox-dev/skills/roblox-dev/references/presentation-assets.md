# Animation, lighting, VFX, audio and asset provenance

## Presentation contract

Use feedback to explain intent, hit/miss/block, threat and reward. Distinguish predicted local cosmetics from accepted server results. Select a coherent visual/audio vocabulary that fits the game fantasy and UI inspirations. Show important cues even with reduced effects or lower quality.

## Animation

Use an Animator created on the server for replicated tracks. Player-owned character animations and non-player animations have different load/start replication requirements; inspect current [Animator](https://create.roblox.com/docs/reference/engine/classes/Animator) documentation. Cache tracks per active Animator where useful; loading repeatedly creates extra tracks. Invalidate caches and marker callbacks on respawn/removal.

Specify rig compatibility, priority, blending, looping and interruption. Verify the actual AnimationTrack properties; check property names against the API reference. Markers can coordinate cosmetic timing, while accepted server action windows govern damage. Permissions and loading failures need fallback rather than an assumed working public ID.

## Lighting and effects

Lighting supports style decisions rather than a single mandatory setting. Inspect [lighting](https://create.roblox.com/docs/environment/lighting), including current LightingStyle/quality behavior. Compare indoor/outdoor and representative quality levels. Post-processing should not conceal interactions or warnings.

Use particles, beams, trails and effect layers with intentional lifetime, scale and observers. Prefer local presentation when full server replication is unnecessary. Budget transparent overlap and emitters on target devices, not just instance count. Keep pooling optional and reset all state when reusing effects. See [particles](https://create.roblox.com/docs/effects/particle-emitters). Cleanup must handle cancellation, failed loads and removed targets.

## Audio

Inspect whether the project uses classic Sound/groups or modern audio graphs. Current [audio objects](https://create.roblox.com/docs/audio/objects) support producers, listeners/emitters, effects and wires; new features need the current API. Preserve a working legacy system if migration is outside scope.

Define spatial versus UI/music sounds, mix controls, concurrency limits, ducking when useful, and pause/respawn behavior. Match mute settings to the graph/groups actually producing sound. Audio readiness cannot block gameplay indefinitely. Ended is not the only cleanup path when an asset never loads or a source is destroyed. Verify permissions, attenuation and target-device volume/clarity.

## Assets

Record provenance, license, owner, intended experience, source file, verified asset reference and fallback. Inspect models and embedded scripts before adopting them. A creator's access to an asset is not automatically permission for the experience; asset types have different privacy/grant rules. See [asset permissions](https://create.roblox.com/docs/projects/assets/privacy).

Keep text/localization separate from baked illustrations when possible. Prefer native editable controls for UI; raster artwork can support ornamentation, thumbnails and illustration. Do not claim asset uploads or moderation completed until confirmed. Prepare only authorized assets and keep generated content consistent with the requested art direction.

Preload immediately needed content selectively, examine failures and avoid a permanent loading gate for optional art. See [ContentProvider](https://create.roblox.com/docs/reference/engine/classes/ContentProvider). Queue counts are not a substitute for a robust completion/failure model.

## Check

Inspect actual in-game views, lower quality and reduced effects, simultaneous animations, death/removal mid-effect, missing/denied assets, audio settings, cancellation and repeated mount/unmount. Record what was seen; an attractive asset preview does not prove a complete gameplay presentation path.

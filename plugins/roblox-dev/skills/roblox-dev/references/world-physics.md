# World layout, terrain, physics and streaming

## Design for the mechanic

Graybox a complete player route from spawn to objective, payoff and retry using actual movement/jump/camera/interaction ranges. Test with intended player counts. Use landmarks, silhouettes and readable contrast to communicate routes. Cover/sightlines matter to combat, restart distance to obbies, legible threat cues to horror, and buildable space/ownership to tycoons. Do not apply one world layout to all genres.

Use semantic zones and reusable models with intentional pivots. Anchored static geometry and simplified decorative collision can reduce unnecessary simulation. Preserve geometry needed for gameplay query/occlusion checks. Procedural generation needs a seed policy, bounded region, progress/cancellation and safe spawn/traversal evidence. Never clear an existing map globally to install a sample.

Consult [terrain](https://create.roblox.com/docs/parts/terrain) and current [WorldRoot](https://create.roblox.com/docs/reference/engine/classes/WorldRoot) APIs for voxel operations and spatial/collision management. Verify current collision-group APIs rather than copying a legacy PhysicsService recipe. Define which layers collide, query, and generate touch events; these properties have different purposes.

## Physics authority

Assign ownership by the intended assembly and gameplay purpose. Client ownership may improve vehicle/player responsiveness, but client-simulated contact/movement is not proof for rewards or damage. Critical objects may warrant server ownership with measured load tradeoffs. Restore automatic ownership when appropriate on exit/reset and test driver/passenger handoff. Anchored and changing assemblies require current constraints/ownership behavior checks. See [network ownership](https://create.roblox.com/docs/physics/network-ownership).

Use modern supported constraints or impulses for physical movement. Avoid old BodyMover snippets as a default. Choose physical simulation versus deliberate placement rather than CFrame-warping bodies every render frame. Bound forces, velocities and lifetime, and verify flinging, collisions and loss of owner. See [mover constraints](https://create.roblox.com/docs/physics/mover-constraints).

## Streaming

Treat client Workspace instances as temporarily absent. Stream-out is not identical to destruction; bindings may need to detach and rebind when content returns. Keep durable identities and distant objective coordinates independent of an instance reference. Do not use indefinite WaitForChild to assume the whole world exists locally.

Choose model atomic/persistent behavior only for a bounded dependency, not the entire map. Streaming availability and nearby physics simulation are distinct. See [instance streaming](https://create.roblox.com/docs/workspace/streaming). Ensure teleports/spawns do not strand players in missing collision geometry under the project's current streaming behavior.

## Check

Test realistic camera views, crowded routes, bounds/spawn safety, collision/query consistency, low graphics quality, ownership handoff, streaming away/returning, reset cleanup and distant world markers. Profile before prescribing universal part, triangle, player or frame budgets. Continue to [presentation-assets.md](presentation-assets.md) for world style and [performance.md](performance.md) for measurement.

## Streaming controls (verify in the docs)

When StreamingEnabled is on, look at `Player.ReplicationFocus`, `Player:RequestStreamAroundAsync` (pre-load an area before teleporting or a cutscene), `Model.ModelStreamingMode` (atomic or persistent models) and `Workspace.StreamingIntegrityMode` (pause behavior when content is missing).

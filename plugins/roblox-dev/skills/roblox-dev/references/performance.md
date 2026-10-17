# Evidence-driven performance

Clarify the symptom and context: client/server, device, build, quality setting, player/NPC population, scene, session age and action. Separate loading delays, sustained frame cost, isolated stutters, network latency and memory growth. Set project-specific targets; no universal triangle, part, memory or FPS threshold establishes quality.

## Measurement loop

Capture a reproducible baseline. Identify the largest meaningful subsystem cost, form one hypothesis, make a focused change, and remeasure the same path plus a representative worst case. Report units, sampling/window and hardware. Studio/emulation is not a low-end hardware benchmark. Average FPS can hide harmful spikes.

Consult [identifying issues](https://create.roblox.com/docs/performance-optimization/identify), [MicroProfiler](https://create.roblox.com/docs/performance-optimization/microprofiler), [improving performance](https://create.roblox.com/docs/performance-optimization/improve), and [designing for performance](https://create.roblox.com/docs/performance-optimization/design). Optimization can trade memory, network, GPU, CPU and response time; preserve correctness and visible behavior.

| Cost | Candidate diagnosis | Preserve |
| --- | --- | --- |
| Script CPU | Expensive scans, frequency, duplicate listeners, burst creation | Authority, timing and relevant targets |
| GPU/rendering | Camera-visible transparency, particles, lights, asset variety | Gameplay tells and intended style |
| Physics | Dynamic assemblies, collisions, ownership, constraints | Correct movement/contact/query semantics |
| Network | Payload size/frequency, replication scope, unnecessary updates | Consequential delivery and resynchronization |
| Memory | Retained references, tasks/connections, previews, caches/pools | Useful reuse and bounded capacity |
| Loading | Critical asset/data readiness, bulk initialization | Recoverable failure and playable progression |

Use events when state changes; retain continuous updates where camera/simulation genuinely needs them. Stage bulk work and throttle relevant sets. Pool or virtualize when measured allocation/layout cost justifies complexity; reset pooled state. Repeated open/close or spawn/despawn baseline/action/baseline comparisons help investigate leaks, while legitimate caches may remain resident.

## Studio profiling guidance

If the Studio connection exposes Roblox-authored profiling or scene-analysis guidance, fetch it before using those tools. Plugin/Studio APIs are not automatically available in normal game scripts. Preserve existing sessions and instrumentation; add only task-owned scopes/probes and remove them when appropriate.

Interpret sample context: parallel scope sums are not elapsed wall time, scene composition can depend on view, automatic script scopes may not identify individual scripts, and unparented instances can be legitimate pools rather than leaks. Capture the interesting window instead of allowing a live ring buffer to overwrite it. Analyze spikes separately from averages.

## Verify and report

Same action before/after, realistic population/content, long session and repeated cleanup, target devices if available. State unavailable hardware or runtime evidence. Do not rename code "optimized" because a property count fell or a single editor view looked faster.

## First tools to reach for

Developer Console (memory, script activity, network), MicroProfiler for frame cost, `debug.profilebegin` / `debug.profileend` to label your own code in the profiler, the `Stats` service for runtime numbers, Actors and parallel Luau for heavy independent work. Measure before and after a change on the target device class. Leak patterns to check: connections never disconnected, instances never destroyed, tables that only grow, per-player state not cleared on leave.

---
name: performance
description: Find and fix Roblox performance problems: lag, memory growth, network cost, slow loading. Use when the user reports lag, low FPS, memory leaks or heavy scripts.
argument-hint: "[system or symptom]"
---

# /roblox-dev:performance

Task: $ARGUMENTS (if empty, ask for the symptom and target device, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/performance.md, ../roblox-dev/references/world-physics.md (streaming).

1. Measure or collect evidence first (microprofiler notes, memory/ping observations, script activity); do not optimize by guess.
2. Rank causes by impact; fix the clear ones with minimal changes (batching, throttling, pooling, disconnecting, streaming).
3. Re-check the original symptom once. Do not claim device numbers you did not measure.

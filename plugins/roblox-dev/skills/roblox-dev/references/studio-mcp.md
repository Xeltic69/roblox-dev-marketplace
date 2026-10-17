# Working with Studio through MCP

This plugin does not ship or replace an MCP server. Roblox's official Studio MCP server (see its [docs](https://create.roblox.com/docs/studio/mcp)) or a community one provides the tools; read their names and schemas from the live connection, never from memory, and never hard-code tool lists here. This file only covers how to work with them.

## Safety
- A connected client can read and modify open places. Confirm which Studio instance and place you are editing before the first write; with several Studio windows open, list the instances and use the right one.
- Do not edit a place the user is actively working in without saying so. Prefer read-only calls until the target is confirmed.
- Never leave test instances, scripts or debug output in the place.
- A listed tool is not proof of an active connection. If calls fail, fall back to offline mode: complete source, exact placement (container, script type, name), initialization order, and the checks still required. Say plainly that nothing was run.

## Working pattern
1. **Inspect first:** studio state, shallow then deeper tree reads, instance properties for the relevant containers, and a search for the names of remotes, attributes and tags before changing anything. Search results are usually capped, so narrow the query instead of assuming you saw everything.
2. **Edit minimally:** read the current script source, apply small targeted edits, re-read the changed range. Put new scripts where the architecture rules say ([architecture conventions](architecture-conventions.md)).
3. **Batch structural changes** (folders, tags, properties) in one Luau execution in the edit context that returns a checkable summary.
4. **Verify with one focused playtest (more only for scenarios the task names):** start play, read the console, optionally capture the viewport, stop play. Use the client context for client behavior and the server context for server state. Edit-time and play-time datamodels are separate: changes made while playing are lost, so persist source changes in edit mode.
5. **Subagents** (if offered) for read-only investigation or scripted gameplay scenarios: give a narrow brief and verify their claims against console output or state.
6. **Input simulation** suits flows that need a real input path (tutorial, shop, prompts), not server-rule validation.
7. **Roblox-authored references** exposed by the server (debugging, device simulation, doc search) beat recalling APIs from memory for new or version-dependent APIs.

## Community servers
Other servers expose different tools (runtime debugging, multiplayer playtests, profiling). Map to their live schema and do not assume feature parity with the official one.

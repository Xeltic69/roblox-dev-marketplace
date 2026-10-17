---
name: backup
description: Export all scripts and a tree listing of a Roblox place before risky changes. Use when the user asks for a backup or before a restructure.
argument-hint: "[target folder]"
disable-model-invocation: true
---

# /roblox-dev:backup

Task: $ARGUMENTS (if empty, ask for the target folder, if no project folder is evident).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/tooling.md.

Export every Script, LocalScript and ModuleScript source (path preserved) plus a tree listing of the other containers to a timestamped folder `_backup/YYYYMMDD-HHMMSS` (no colons, so it is valid on Windows). Include attributes and tags of the instances in the tree listing. A target outside the project folder needs the owner's approval. If the project is Rojo- or git-managed, prefer a commit or copy of the sources over re-exporting. Never overwrite an existing backup. Ask for the target folder if there is no obvious project directory, and remind the owner to add `_backup/` to `.gitignore`. Also remind them to save a copy of the place file (File > Save As): script exports do not capture UI, models or terrain. Warn that scripts can contain secrets, so the backup must not be published. Change nothing in the place.

# Memory Sync Policy

Last updated: 2026-06-06 Asia/Shanghai

## User Preference

Whenever the user mentions memory/记忆 in any form, Codex should understand memory as a linked system, not a single file.

The linked memory system includes these exact paths:

1. Local project memory version: `D:\文档\前端\skills\codex-memory\references\memory.md`
2. Global Codex memory version: `C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md`
3. GitHub memory archive: `kiwa18/oracle-agent/memory/**`, starting from `kiwa18/oracle-agent/memory/INDEX.md`

These three layers should be considered connected and should be kept aligned when memory is read or updated.

## Layer Roles

### 1. Local Project Memory Version

Purpose:

- quick context
- recent preferences
- active tasks
- local pointers to GitHub detail files
- the editable source copy of memory Skills when available

Exact memory file:

- `D:\文档\前端\skills\codex-memory\references\memory.md`

Exact Skill folder:

- `D:\文档\前端\skills\codex-memory`

Codex should update this D-drive project version first when it is writable. The user will manually copy or merge this project version to the C-drive global version when needed.

### 2. C-drive Global Codex Memory Version

Purpose:

- installed global Skill copy loaded by Codex across sessions
- runtime trigger and recovery point

Exact memory file:

- `C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md`

Exact Skill folder:

- `C:\Users\ASUS\.codex\skills\codex-memory`

If Codex updates the D-drive project/source Skill but cannot write to this C-drive path due to sandbox permissions, Codex must remind the user to manually copy or merge:

- from `D:\文档\前端\skills\codex-memory`
- to `C:\Users\ASUS\.codex\skills\codex-memory`

### 3. GitHub Memory Archive

Purpose:

- durable project architecture
- detailed decisions
- research records
- reusable policy and Skill documentation
- project-level continuation files

Known GitHub paths:

- `kiwa18/oracle-agent/memory/INDEX.md`
- `kiwa18/oracle-agent/memory/projects/**`
- `kiwa18/oracle-agent/memory/policies/**`

## Read Rule

When memory is triggered:

1. Read local quick memory first from `D:\文档\前端\skills\codex-memory\references\memory.md` when available.
2. If the question is project-related or local memory is not enough, read the GitHub memory index and the smallest relevant GitHub detail file.
3. Treat C-drive global memory as the installed runtime copy; if it appears stale, mention that it may need syncing from the D-drive project/source copy.

## Update Rule

When saving memory:

1. Update D-drive local project/source memory first if writable: `D:\文档\前端\skills\codex-memory\references\memory.md`.
2. Update GitHub memory for durable project details, policies, architecture, research, and reusable records.
3. Update C-drive global memory too if writable: `C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md`.
4. If C-drive global memory is not writable, explicitly remind the user to sync it manually from `D:\文档\前端\skills\codex-memory` to `C:\Users\ASUS\.codex\skills\codex-memory`.
5. Do not silently update only one layer when the information belongs in more than one layer.

## Main Priority

- D-drive local project memory is the quick index and editable source in this workspace.
- GitHub memory is the long-term source of detailed truth.
- C-drive global memory is the installed runtime copy that should stay aligned with the D-drive source and GitHub archive.

## Encoding Note

Keep memory files as UTF-8 text. Avoid rewriting whole files through shell commands that may use a legacy Windows code page and corrupt Chinese text. Prefer targeted patches or UTF-8-aware editors.

## Safety

Do not store secrets, tokens, API keys, passwords, cookies, private auth material, or sensitive private data in any memory layer.

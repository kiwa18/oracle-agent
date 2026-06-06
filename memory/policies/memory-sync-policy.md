# Memory Sync Policy

Last updated: 2026-06-06 Asia/Shanghai

## User Preference

Whenever the user mentions memory/记忆 in any form, Codex should understand memory as a linked system, not a single file.

The linked memory system includes:

1. Local workspace or E-drive memory source
2. C-drive global Codex Skill memory
3. GitHub memory archive under `kiwa18/oracle-agent/memory/**`

These three layers should be considered connected and should be kept aligned when memory is read or updated.

## Layer Roles

### 1. Local Workspace / E-drive Memory Source

Purpose:

- quick context
- recent preferences
- active tasks
- local pointers to GitHub detail files
- the editable source copy of memory Skills when available

Known current workspace source:

- `D:\文档\前端\skills\codex-memory`

The user may refer to this layer as local E-drive memory. If the user provides a specific E-drive memory path later, add it to this policy and treat it as part of the local source layer.

### 2. C-drive Global Codex Memory

Purpose:

- installed global Skill copy loaded by Codex across sessions
- runtime trigger and recovery point

Known global path:

- `C:\Users\ASUS\.codex\skills\codex-memory`

If Codex updates the workspace/source Skill but cannot write to this C-drive path due to sandbox permissions, Codex must remind the user to manually copy or merge the workspace/source Skill into the C-drive global Skill directory.

### 3. GitHub Memory Archive

Purpose:

- durable project architecture
- detailed decisions
- research records
- reusable policy and Skill documentation
- project-level continuation files

Known GitHub index:

- `kiwa18/oracle-agent/memory/INDEX.md`

## Read Rule

When memory is triggered:

1. Read local quick memory first when available.
2. If the question is project-related or local memory is not enough, read the GitHub memory index and the smallest relevant GitHub detail file.
3. Treat C-drive global memory as the installed runtime copy; if it appears stale, mention that it may need syncing from the workspace/source copy.

## Update Rule

When saving memory:

1. Update local workspace/source memory first if writable.
2. Update GitHub memory for durable project details, policies, architecture, research, and reusable records.
3. Update C-drive global memory too if writable.
4. If C-drive global memory is not writable, explicitly remind the user to sync it manually.
5. Do not silently update only one layer when the information belongs in more than one layer.

## Main Priority

- Local memory is the quick index and current working context.
- GitHub memory is the long-term source of detailed truth.
- C-drive global memory is the installed runtime copy that should stay aligned with the source and GitHub archive.

## Safety

Do not store secrets, tokens, API keys, passwords, cookies, private auth material, or sensitive private data in any memory layer.

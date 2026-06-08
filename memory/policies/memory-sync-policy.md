# Memory Sync Policy

Last updated: 2026-06-08 Asia/Shanghai

## User Preference

Whenever the user mentions memory/记忆 in any form, Codex should understand memory as a linked system, not a single file.

The linked memory system includes these exact layers:

1. E-drive local project/source memory package: `E:\codex\skills-memory`
2. C-drive global Codex runtime skills: `C:\Users\ASUS\.codex\skills`
3. GitHub memory archive: `kiwa18/oracle-agent/memory/**`, starting from `kiwa18/oracle-agent/memory/INDEX.md`

These layers should be considered connected and should be kept aligned when memory is read or updated.

## Tree Structure

See the full tree map in:

- `memory/STRUCTURE.md`

Local E-drive structure:

```text
E:\codex\skills-memory
├─ codex-memory
│  ├─ SKILL.md
│  └─ references
│     ├─ memory.md
│     ├─ daily.md
│     └─ prompts.md
├─ gpt-architecture-review
└─ real-time-context
```

C-drive global runtime structure:

```text
C:\Users\ASUS\.codex\skills
├─ .system
├─ codex-memory
├─ gpt-architecture-review
└─ real-time-context
```

GitHub archive structure:

```text
kiwa18/oracle-agent/memory
├─ INDEX.md
├─ STRUCTURE.md
├─ projects
└─ policies
```

## Layer Roles

### 1. E-drive Local Project/Source Memory

Purpose:

- quick context
- recent preferences
- active tasks
- local pointers to GitHub detail files
- editable source copy of user-maintained Skills
- daily and prompt memory files

Exact local quick memory file:

- `E:\codex\skills-memory\codex-memory\references\memory.md`

Related local memory files:

- `E:\codex\skills-memory\codex-memory\references\daily.md`
- `E:\codex\skills-memory\codex-memory\references\prompts.md`

Exact local Skill folders:

- `E:\codex\skills-memory\codex-memory`
- `E:\codex\skills-memory\gpt-architecture-review`
- `E:\codex\skills-memory\real-time-context`

Codex should update this E-drive source package first when it is writable.

### 2. C-drive Global Codex Runtime Skills

Purpose:

- installed global Skill copy loaded by Codex across sessions
- runtime trigger and recovery point

Exact global memory file:

- `C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md`

Exact global Skill folders:

- `C:\Users\ASUS\.codex\skills\codex-memory`
- `C:\Users\ASUS\.codex\skills\gpt-architecture-review`
- `C:\Users\ASUS\.codex\skills\real-time-context`

If Codex updates E-drive but cannot write to C-drive due to sandbox permissions, Codex must remind the user to manually sync from `E:\codex\skills-memory` to `C:\Users\ASUS\.codex\skills`.

### 3. GitHub Memory Archive

Purpose:

- durable project architecture
- detailed decisions
- research records
- reusable policy and Skill documentation
- project-level continuation files
- tree index and memory sync policy

Known GitHub paths:

- `kiwa18/oracle-agent/memory/INDEX.md`
- `kiwa18/oracle-agent/memory/STRUCTURE.md`
- `kiwa18/oracle-agent/memory/projects/**`
- `kiwa18/oracle-agent/memory/policies/**`

## Read Rule

When memory is triggered:

1. Read E-drive local quick memory first when available: `E:\codex\skills-memory\codex-memory\references\memory.md`.
2. Read `daily.md` when the question involves tone, habits, ordinary preferences, workflow friction, or long-term familiarity.
3. Read `prompts.md` when the question involves reusable prompts, GPT/Claude review, memory-save templates, migration checks, or Skill wording.
4. If the question is project-related or local memory is not enough, read the GitHub memory index and the smallest relevant GitHub detail file.
5. Treat C-drive global memory as the installed runtime copy; if it appears stale, mention that it may need syncing from E-drive source and GitHub archive.

## Update Rule

When saving memory:

1. Update E-drive local project/source memory first if writable.
2. Update GitHub memory for durable project details, policies, architecture, research, and reusable records.
3. Update C-drive global memory too if writable.
4. If E-drive or C-drive is not writable, explicitly remind the user which layer still needs manual sync.
5. Do not silently update only one layer when the information belongs in more than one layer.

## Append-First Rule

Memory should not be casually deleted, cleared, or overwritten.

Default behavior:

- Prefer appending dated entries, corrections, or new structured sections.
- Preserve older useful context unless the user explicitly asks to remove or replace it, or it is clearly unsafe to keep.
- For corrections, add a dated correction entry when the historical trail is useful.
- Ask before deleting memory files, clearing sections, or overwriting large parts of any memory layer.
- If the user did not explicitly ask for replacement, Codex must not delete or reduce memory; it may only structure and add.

## Main Priority

- E-drive local memory is the quick index and editable source package.
- GitHub memory is the long-term source of detailed truth and structure.
- C-drive global memory is the installed runtime copy that should stay aligned with E-drive source and GitHub archive.

## Encoding Note

Keep memory files as UTF-8 text. Avoid rewriting whole files through shell commands that may use a legacy Windows code page and corrupt Chinese text. Prefer targeted patches or UTF-8-aware editors.

## Safety

Do not store secrets, tokens, API keys, passwords, cookies, private auth material, or sensitive private data in any memory layer.

# Memory Structure

Last updated: 2026-06-08 Asia/Shanghai

This file is the tree index for the linked Codex memory system. Use it to find the right memory file quickly without mixing project memory, daily preferences, prompts, and policy rules.

## Three Linked Indexes

The memory system has three linked indexes. Keep all three aligned:

```text
E-drive source index
E:\codex\skills-memory\STRUCTURE.md
E:\codex\skills-memory\codex-memory\references\memory.md
```

```text
C-drive runtime index
C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md
```

```text
GitHub durable index
kiwa18/oracle-agent/memory/INDEX.md
kiwa18/oracle-agent/memory/STRUCTURE.md
kiwa18/oracle-agent/memory/policies/memory-sync-policy.md
```

When updating durable preferences, architecture rules, or memory structure, update E-drive and GitHub first when possible, then remind the user to sync C-drive if Codex cannot write it.

## Local / Global / GitHub Layers

```text
E:\codex\skills-memory
├─ STRUCTURE.md
├─ codex-memory
│  ├─ SKILL.md
│  ├─ agents
│  │  └─ openai.yaml
│  └─ references
│     ├─ memory.md    # main local index, project memory, path rules, open tasks
│     ├─ daily.md     # ordinary preferences, tone, rhythm, collaboration habits
│     └─ prompts.md   # reusable GPT/Claude/review/memory prompt templates
├─ gpt-architecture-review
│  ├─ SKILL.md        # architecture review and 3-failure GPT diagnosis rule
│  └─ agents
│     └─ openai.yaml
└─ real-time-context
   ├─ SKILL.md        # current-time, latest facts, source/date authenticity rule
   └─ agents
      └─ openai.yaml
```

```text
C:\Users\ASUS\.codex\skills
├─ .system            # Codex system skills, do not delete
├─ codex-memory       # installed global runtime memory skill
├─ gpt-architecture-review
└─ real-time-context
```

```text
kiwa18/oracle-agent/memory
├─ INDEX.md           # short entry index
├─ STRUCTURE.md       # this tree map
├─ projects
│  └─ a-share-event-backtest.md
└─ policies
   ├─ browser-connection-preferences.md
   ├─ daily-collaboration-memory.md
   ├─ github-operation-preferences.md
   ├─ gpt-architecture-review.md
   ├─ memory-sync-policy.md
   ├─ prompt-memory.md
   └─ real-time-context.md
```

## What To Read

- For quick current context: `E:\codex\skills-memory\codex-memory\references\memory.md`.
- For tone, habits, and everyday collaboration: `E:\codex\skills-memory\codex-memory\references\daily.md` and GitHub `memory/policies/daily-collaboration-memory.md`.
- For prompt templates: `E:\codex\skills-memory\codex-memory\references\prompts.md` and GitHub `memory/policies/prompt-memory.md`.
- For A-share event backtest architecture: GitHub `memory/projects/a-share-event-backtest.md`.
- For Chrome connection rules: GitHub `memory/policies/browser-connection-preferences.md`.
- For architecture review and 3-failure GPT diagnosis: local `gpt-architecture-review` Skill and GitHub `memory/policies/gpt-architecture-review.md`.
- For real-time/date/source authenticity: local `real-time-context` Skill and GitHub `memory/policies/real-time-context.md`.
- For memory sync rules: GitHub `memory/policies/memory-sync-policy.md`.

## Update Discipline

- Default update behavior is append-first and structure-first.
- Unless the user explicitly requests replacement, do not delete or reduce memory. Add dated entries or new structured sections instead.
- For durable rules and project decisions, update both the E-drive local memory package and GitHub memory.
- If Codex cannot write E-drive directly, update GitHub and remind the user to sync the E-drive local files.
- If Codex cannot write C-drive global memory directly, remind the user to sync from `E:\codex\skills-memory` to `C:\Users\ASUS\.codex\skills`.
- Do not silently let E-drive local memory and GitHub memory drift.

## Changelog

- 2026-06-08: Created tree index for local, global, and GitHub memory structure.
- 2026-06-08: Added explicit three-linked-index section for E-drive, C-drive, and GitHub memory indexes.

# Memory Index

Last updated: 2026-06-08 Asia/Shanghai

This directory is the GitHub long-term memory layer for Codex and other AI agents. Use this file as the short entry index, then use `memory/STRUCTURE.md` for the full tree map.

## Three Linked Indexes

Keep these three indexes aligned:

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

## Start Here

- Full tree map: `memory/STRUCTURE.md`
- E-drive local quick memory: `E:\codex\skills-memory\codex-memory\references\memory.md`
- C-drive global runtime memory: `C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md`
- GitHub archive root: `kiwa18/oracle-agent/memory/**`

## Trigger Phrases

When the user says any of the following, read the relevant memory before answering or continuing work:

- `继续回测输出`
- `继续回策输出`
- `继续A股回测`
- `调出回测记忆`
- `读取GitHub记忆`
- `看回测架构`
- `记忆`
- `记住`
- `记录`
- `记忆存档`
- `存入记忆`
- `登录前看记忆`
- `开始前看记忆`
- `看一下记忆`

## Local Memory Files

```text
E:\codex\skills-memory\codex-memory\references
├─ memory.md   # main quick index, path rules, project pointers
├─ daily.md    # daily preferences, rhythm, tone, familiarity
└─ prompts.md  # reusable GPT/Claude/review/memory prompt templates
```

## Skill Packages

```text
E:\codex\skills-memory
├─ STRUCTURE.md
├─ codex-memory
├─ gpt-architecture-review
└─ real-time-context
```

Installed global skill path:

```text
C:\Users\ASUS\.codex\skills
├─ codex-memory
├─ gpt-architecture-review
└─ real-time-context
```

## Project Memory Files

### A-share Event Backtest

- File: `memory/projects/a-share-event-backtest.md`
- Status: architecture and research memory created
- Core idea: the TongDaXin indicator only provides buy-point signals. Do not assume same-day buying and do not invent a sell indicator in V1. Treat every signal as an event origin, then study future path windows to find which buy delay and holding/observation windows work best.
- Main data direction: use local TongDaXin historical daily data as the primary price source; use open-source data tools such as `a-stock-data`, `mootdx`, `pytdx`, and `MyTT` as auxiliary components.

## Policy Memory Files

- GitHub operation preferences: `memory/policies/github-operation-preferences.md`
- Memory sync policy: `memory/policies/memory-sync-policy.md`
- Browser connection preferences: `memory/policies/browser-connection-preferences.md`
- Daily collaboration memory: `memory/policies/daily-collaboration-memory.md`
- Prompt memory: `memory/policies/prompt-memory.md`
- GPT architecture review: `memory/policies/gpt-architecture-review.md`
- Real-time context: `memory/policies/real-time-context.md`

## Update Rule

- Keep this index short and use `memory/STRUCTURE.md` for the full tree.
- For durable rules and project decisions, update both E-drive local memory and GitHub memory when possible.
- If Codex cannot write E-drive or C-drive from the current sandbox, update GitHub and remind the user which local layer still needs syncing.
- Unless the user explicitly asks for replacement, do not delete or reduce memory; add structured dated entries instead.
- Do not store private formulas, credentials, tokens, cookies, or full proprietary strategy logic here.

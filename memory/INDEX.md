# Memory Index

Last updated: 2026-06-06 Asia/Shanghai

This directory is the GitHub long-term memory layer for Codex and other AI agents. Local Codex memory should use this file as the entry index when a project question needs durable architecture, research, or decision context.

## How To Use

When the user says any of the following, read the relevant file before answering or continuing work:

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

For A-share signal/backtest work, read:

- `memory/projects/a-share-event-backtest.md`

For GitHub operation preferences and confirmation boundaries, read:

- `memory/policies/github-operation-preferences.md`

For D-drive local project memory / C-drive global memory / GitHub memory linkage and sync rules, read:

- `memory/policies/memory-sync-policy.md`

## Project Memory Files

### A-share Event Backtest

- File: `memory/projects/a-share-event-backtest.md`
- Status: architecture and research memory created
- Core idea: the TongDaXin indicator only provides buy-point signals. Do not assume same-day buying and do not invent a sell indicator in V1. Treat every signal as an event origin, then study future path windows to find which buy delay and holding/observation windows work best.
- Main data direction: use local TongDaXin historical daily data as the primary price source; use open-source data tools such as `a-stock-data`, `mootdx`, `pytdx`, and `MyTT` as auxiliary components.

## Policy Memory Files

### GitHub Operation Preferences

- File: `memory/policies/github-operation-preferences.md`
- Standing preference: for the GitHub account `kiwa18`, Codex may directly create and update files, directories, and repository content across all accessible repositories and paths without asking each time.
- Ask first only for destructive changes, changes that overwrite/restructure more than roughly one third of a repository's main framework or subject structure, secrets/privacy-sensitive content, repository permission/security changes, or actions where the platform requires confirmation.

### Memory Sync Policy

- File: `memory/policies/memory-sync-policy.md`
- Standing preference: whenever the user mentions memory/记忆, Codex should treat these as linked layers:
  - local project version: `D:\文档\前端\skills\codex-memory\references\memory.md`
  - global version: `C:\Users\ASUS\.codex\skills\codex-memory\references\memory.md`
  - GitHub archive: `kiwa18/oracle-agent/memory/**`
- Update rule: update the D-drive project/source memory and GitHub memory when relevant; update C-drive global memory if writable, otherwise remind the user to manually sync `D:\文档\前端\skills\codex-memory` into `C:\Users\ASUS\.codex\skills\codex-memory`.
- Encoding rule: keep memory files as UTF-8 and avoid shell rewrites that may corrupt Chinese text through a legacy Windows code page.

## Memory Policy

- Keep this index short.
- Put detailed design, decisions, references, and next steps in project-specific files.
- Do not store private formulas, credentials, tokens, or full proprietary strategy logic here.
- If the user later provides the TongDaXin formula, store only the conversion notes and file location unless the user explicitly asks to store the full formula.

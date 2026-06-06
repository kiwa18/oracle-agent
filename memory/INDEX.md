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

For A-share signal/backtest work, read:

- `memory/projects/a-share-event-backtest.md`

## Project Memory Files

### A-share Event Backtest

- File: `memory/projects/a-share-event-backtest.md`
- Status: architecture and research memory created
- Core idea: the TongDaXin indicator only provides buy-point signals. Do not assume same-day buying and do not invent a sell indicator in V1. Treat every signal as an event origin, then study future path windows to find which buy delay and holding/observation windows work best.
- Main data direction: use local TongDaXin historical daily data as the primary price source; use open-source data tools such as `a-stock-data`, `mootdx`, `pytdx`, and `MyTT` as auxiliary components.

## Memory Policy

- Keep this index short.
- Put detailed design, decisions, references, and next steps in project-specific files.
- Do not store private formulas, credentials, tokens, or full proprietary strategy logic here.
- If the user later provides the TongDaXin formula, store only the conversion notes and file location unless the user explicitly asks to store the full formula.

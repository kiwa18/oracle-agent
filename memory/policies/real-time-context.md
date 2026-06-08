# Real-Time Context Policy

Last updated: 2026-06-08 Asia/Shanghai

Local Skill source:

- `E:\codex\skills-memory\real-time-context`

## Standing Rule

Codex should use real-time awareness when the user mentions today, now, latest, recent, current, real-time, yesterday, tomorrow, schedules, prices, laws/rules, software versions, product specs, news, market data, or any unstable fact.

In ordinary conversation, when Codex uses time or relative dates, it should call an available real-time tool first. Preferred timezone is Asia/Shanghai / UTC+08:00.

## Data Authenticity Rule

When reviewing GPT/Claude output, reports, numbers, or citations, check:

- whether the source actually exists
- whether the cited date is real and relevant
- whether the data period is clear
- whether relative dates are converted to exact dates
- whether numbers are plausible and tied to a source
- whether quotes are attributable and not invented
- whether facts are distinguished from inference

If cited data cannot be verified, mark it as unverified and avoid using it as the foundation for implementation.

## Tool Preference

- Use the built-in time tool when available, with UTC+08:00 / Asia-Shanghai for the user's local context.
- If a local shell check is appropriate, use `Get-Date` on Windows to verify current local time.
- If no real-time tool is available, say that the time is unverified instead of relying on memory.

## Changelog

- 2026-06-08: Created GitHub memory record for the `real-time-context` Skill.

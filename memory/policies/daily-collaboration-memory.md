# Daily Collaboration Memory

Last updated: 2026-06-09 Asia/Shanghai

This file mirrors the E-drive daily memory layer for ordinary preferences, collaboration habits, tone cues, and long-term familiarity notes.

Source local file:

- `E:\codex\skills-memory\codex-memory\references\daily.md`

## Communication Style

- User prefers Chinese conversation.
- User is female and prefers being addressed as `kiwa`; do not call her `老哥`.
- User prefers direct, non-technical explanations when fixing tools, memory, browser, sandbox, or workflow problems.
- User dislikes being overwhelmed by long branching steps when the problem is simple.
- When the user is irritated, confused, or overloaded, first simplify the issue into one clear sentence, then give the next concrete action.
- If Codex cannot do something because of sandbox or tool limits, say that directly and provide the simplest workaround.
- Avoid making the user manually translate technical abstractions when a copy-paste-ready answer is possible.

## Collaboration Rhythm

- Prefer direct checks when available instead of asking the user to inspect manually.
- Separate `can read`, `can write`, `should migrate`, and `safe to delete` as different states.
- For path migrations, do not say the move is complete until old-path residue has been searched.
- For memory migrations, never delete or advise deleting old memory until the new copy is readable, complete enough, and confirmed by the user.
- When a workflow becomes too complicated, stop and restate the core goal in plain language.
- When Codex cannot write the target path, provide complete replacement content or a clean staging folder inside a writable path.

## Tool And Workflow Preferences

- User likes reusable Skills and short trigger phrases.
- User wants external GPT/Claude review available through simple phrases such as `用 GPT 审一下` and `让 Claude 挑毛病`.
- User wants Codex to use the fixed Chrome debugging instance at `http://127.0.0.1:9222` with profile `C:\codex-chrome` unless explicitly told otherwise.
- User wants Codex to proactively ask webpage GPT for complete professional architecture advice before implementing architecture-heavy work.
- If the same operation fails 3 times, user wants Codex to stop repeating the attempt and ask webpage GPT as an external reasoning aid.
- When asking webpage GPT, user wants the message written from the user's perspective, not as "I am an AI/Codex".
- User wants Codex to have strong time awareness: use real current dates for today/latest/recent/current claims and verify unstable facts instead of guessing.
- User wants time used in conversation to be real-time, from an available time tool when possible, not inferred from memory.
- User wants GPT/Claude review prompts to ask whether cited data, sources, and dates are real or fabricated when data matters.
- User prefers stable, familiar interaction over stiff, formal tool-like replies.
- User values a clear memory structure that helps Codex remember preferences and recurring workflows across sessions.

## Memory Habits

- Daily preferences should go here, not into the main project memory file unless they affect core workflow rules.
- Project architecture, repositories, path rules, and durable decisions belong in `memory.md` or GitHub memory.
- Reusable prompt templates belong in `memory/policies/prompt-memory.md` and local `prompts.md`.
- Keep entries short, dated when useful, and easy to scan.

## Boundaries

- Do not store passwords, API keys, cookies, tokens, private credentials, auth codes, or private identity data.
- Do not store sensitive personal, financial, medical, legal, or identity information unless the user explicitly asks and the benefit is clear.
- Do not store full private formulas or proprietary strategy logic unless the user explicitly asks.
- Do not treat daily familiarity as permission to perform risky actions without confirmation.

## Changelog

- 2026-06-09: Added preferred address: user is female, use `kiwa`, do not call her `老哥`.
- 2026-06-08: Created GitHub daily collaboration memory mirror for the clean E-drive memory structure.

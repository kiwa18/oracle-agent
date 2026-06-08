# Browser Connection Preferences

Last updated: 2026-06-08 Asia/Shanghai

## User Preference

For Chrome-related Codex work, default to the user's existing Chrome debugging instance instead of automatically creating a new built-in Chrome or temporary browser.

Fixed debugging address:

- `http://127.0.0.1:9222`

Fixed AI Chrome profile:

- `C:\codex-chrome`

## Practical Rule

Default behavior:

- Prefer reusing the Chrome instance launched by the user with remote debugging on port `9222`.
- Treat `C:\codex-chrome` as the fixed AI Chrome profile for this workflow.
- Do not automatically create a new built-in Chrome, temporary Chrome profile, or separate browser unless the user explicitly asks.
- If the `9222` instance is unavailable, report that clearly and ask the user whether to launch or reconnect it.

## Boundary

This preference does not authorize reading passwords, cookies, browser history, unrelated tabs, account menus, secrets, tokens, or private authentication material. Browser discovery should stay read-only unless the user asks for a specific action.

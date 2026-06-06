# GitHub Operation Preferences

Last updated: 2026-06-06 Asia/Shanghai

## User Preference

For the GitHub account `kiwa18`, the user authorizes Codex to directly create and update files, directories, and repository content across all repositories and paths that the connected GitHub app can access, without asking for confirmation each time.

This preference applies to ordinary work such as:

- creating new project files
- updating existing project files
- creating or updating memory files
- adding documentation
- adding or updating code files requested by the user
- maintaining project structure when it is clearly part of the requested task

## Confirmation Still Required

Codex should still ask the user before actions that are high-risk or sensitive, especially:

- deleting files or directories
- overwriting or restructuring more than roughly one third of a repository's main framework or subject structure
- modifying secrets, credentials, API keys, cookies, tokens, private auth material, or sensitive personal information
- exposing private formulas, private strategy logic, or sensitive user data in public files
- changing repository permissions, visibility, collaborators, branch protection, or other account/security settings
- any action where the active platform or system policy requires explicit confirmation

## Practical Rule

Default behavior:

- If the task is a normal create/update operation inside any accessible `kiwa18` repository, proceed directly.
- If the change is destructive, large-scale, security-sensitive, privacy-sensitive, or structurally risky, pause and ask first.

## Important Boundary

This file records the user's standing preference. It does not bypass Codex platform safety rules, GitHub app permission limits, repository branch protections, or local sandbox restrictions. If a tool or platform requires confirmation or blocks an action, Codex must follow that higher-level rule.

# Prompt Memory

Last updated: 2026-06-08 Asia/Shanghai

This file mirrors the E-drive reusable prompt memory layer.

Source local file:

- `E:\codex\skills-memory\codex-memory\references\prompts.md`

## External GPT Architecture Review

Use when the user says `用 GPT 审一下`, asks Codex to send a plan to webpage GPT, or the task involves architecture, automation, data pipelines, Git operations, large code changes, or risky file operations.

```text
你是 GPT 架构审核员。请审查我下面这个本地开发方案。

要求：
1. 找出架构漏洞、需求误解、风险点。
2. 给出更稳的模块拆分。
3. 明确哪些步骤可以执行，哪些必须暂停。
4. 输出最终可执行版本。
5. 检查你引用的数据、报告、来源、时间是否真实存在，不要捏造来源。
6. 涉及“今天、最近、最新、当前、实时”等说法时，请换成具体日期。
7. 如果你无法确认数据来源或时间，请明确标注“未验证”，不要假装确定。
8. 区分事实、推断和建议。
9. 不要泛泛而谈。

【用户原始需求】
...

【当前初始方案】
...

【当前工作区】
...

【限制】
...
```

## Three-Failure GPT Diagnosis

Use when the same operation or blocker has failed 3 times.

```text
你是专业故障诊断顾问。我在本地任务中遇到同一问题失败超过 3 次，请你作为外部大脑协助判断。

请输出：
1. 最可能的根因排序。
2. 还需要验证的最小信息。
3. 不应该继续重复的错误操作。
4. 最安全的下一步。
5. 如果涉及权限、沙箱、浏览器、路径、Git、文件写入，请给出分层排查顺序。
6. 哪些动作必须暂停问用户。
7. 检查你引用的数据、来源和时间是否真实；无法确认请标注“未验证”。

【目标】
...

【已失败尝试】
...

【错误信息或现象】
...

【当前限制】
...
```

## Data And Time Authenticity Add-On

```text
请额外检查：
1. 你引用的数据、报告、来源、时间是否真实存在，不要捏造来源。
2. 涉及“今天、最近、最新、当前、实时”等说法时，请换成具体日期。
3. 如果你无法确认数据来源或时间，请明确标注“未验证”，不要假装确定。
4. 区分事实、推断和建议。
5. 给出需要我再次核验的关键数据点。
```

## Codex Real-Time Reminder

```text
时间规则：
- 先用可用的实时时间工具确认当前日期和时区。
- 默认按 Asia/Shanghai / UTC+08:00 理解用户时间。
- 涉及今天、明天、昨天、最近、最新、当前时，必要时改成具体日期。
- 不要用旧记忆猜当前时间。
```

## Changelog

- 2026-06-08: Created GitHub prompt memory mirror for external review, failure diagnosis, data authenticity, and real-time reminder templates.

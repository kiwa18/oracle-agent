# 全局记忆索引模板

> 启动时自动加载。写清每个文件的用途、读写权限。需要什么内容就去对应文件搜。

## 一、CODE 记忆区（传输审核层）

**目录**：`-home-ubuntu-xiaoke/memory/`
**规则**：CODE 可读写，Claude 只读

| 文件 | 格式 | 用途 | ✏️ 写 | 👁 读 |
|------|:---:|------|:---:|:---:|
| `role-guard.md` | MD | CODE 角色锁 | 手动 | 双方 |
| `session-handoff.md` | MD | 上次聊到哪、待办 | CODE | 双方 |
| `task-log.md` | MD | 任务档案 | CODE | 双方 |
| `wechat-memory.jsonl` | JSONL | 微信重要记忆 | CODE | 双方 |
| `user-profile.md` | MD | 用户偏好 | 双方 | 双方 |

## 二、Claude 记忆区（数据落实层）

**目录**：`-home-ubuntu/memory/`
**规则**：Claude 可读写，CODE 只读

| 文件 | 格式 | 用途 | ✏️ 写 | 👁 读 |
|------|:---:|------|:---:|:---:|
| `MEMORY_INDEX.md` | MD | 本文件：全局记忆地图 | Claude | 双方 |
| `code-claude-framework.md` | MD | 协作框架 | Claude | 双方 |
| `data-source-log.md` | MD | 数据接口状态 | Claude | 双方 |
| `task-result-cache.md` | MD | 任务结果存根 | Claude | 双方 |
| `user-profile.md` | MD | 用户偏好 | 双方 | 双方 |
| `trading-agent-project-framework.md` | MD | QPSM 项目结构 | Claude | 双方 |
| `kline_patterns.md` | MD | K线形态规则库 | Claude | 双方 |
| `deepseek_preference.md` | MD | DeepSeek API 配置 | Claude | 双方 |
| `mobile_frontend.md` | MD | 手机Web前端 | Claude | 双方 |

## 三、Trading Agent 记忆区

**目录**：`-home-ubuntu-trading-agent/memory/`
**规则**：Claude 可读写，CODE 只读

| 文件 | 格式 | 用途 | ✏️ 写 | 👁 读 |
|------|:---:|------|:---:|:---:|
| `next-session-handoff.md` | MD | 交易项目进度 | Claude | 双方 |
| `project-setup.md` | MD | 项目全貌 | Claude | 双方 |
| `coding-mindset.md` | MD | TDX翻译思维 | Claude | 双方 |
| `security-policy.md` | MD | 安全检查规则 | Claude | 双方 |
| `2026-06-13-session.md` | MD | 历史会话 | Claude | 双方 |
| `codex-unavailability.md` | MD | Codex 不可用 | Claude | 双方 |

## 四、检索关键词映射

| 想查什么 | 去哪个文件 |
|------|------|
| 上次聊到哪 | CODE区 session-handoff.md |
| 任务跑了没有 | CODE区 task-log.md |
| 用户说过的事 | CODE区 wechat-memory.jsonl |
| 上次用的什么接口 | Claude区 data-source-log.md |
| 上次结果 | Claude区 task-result-cache.md |
| 怎么分工的 | Claude区 code-claude-framework.md |
| K线形态规则 | Claude区 kline_patterns.md |
| QPSM怎么跑 | Claude区 trading-agent-project-framework.md |
| 交易项目上次进度 | Trading区 next-session-handoff.md |

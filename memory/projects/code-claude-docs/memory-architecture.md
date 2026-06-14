# 记忆分层与隔离设计

## 设计原则

**CODE 记住人，Claude 记住活。**

| 角色 | 记忆范围 | 核心问题 |
|------|----------|----------|
| CODE | 用户、对话、任务状态 | "上次聊到哪了" "用户喜欢什么" |
| Claude | 数据、接口、规则 | "上次用了哪个接口" "K线形态怎么判" |

## 三层记忆模型

```
角色层（不可写） → role-guard.md
  ↓ 定义你是谁，永远不变
会话层（跨会话） → session-handoff.md, task-log.md
  ↓ 上次进行到哪，任务状态
用户层（长期）   → user-profile.md, wechat-memory.jsonl
  ↓ 用户偏好，微信重要记忆
```

## 隔离机制

### 目录隔离

CODE 区和 Claude 区是不同目录，bridge 通过 `MEMORY_DIR` 指向 CODE 区，`_load_context()` 只加载 CODE 区文件 + 全局索引。

### 角色锁

CODE 启动时加载 `role-guard.md`，明确"你不是 Codex 协作者，不写代码不碰数据"。同时项目级 `CLAUDE.md` 覆盖全局 Codex 协作规则。

### 写权限隔离

- CODE 绝不写 Claude 区、Trading 区文件
- Claude 绝不写 CODE 区文件
- 公用 `user-profile.md` 双方都写

### 启动加载隔离

- CODE 不加载全局 CLAUDE.md（通过项目 CLAUDE.md + role-guard.md 覆盖）
- CODE 不加载 trading-agent memory
- CODE 不加载 kline_patterns 等技术规则

## 文件详细说明

### CODE 区（5 个文件）

| 文件 | 加载时机 | 更新时机 | 内容 |
|------|----------|----------|------|
| role-guard.md | 每次启动 | 手动 | CODE 身份定义 |
| session-handoff.md | 每次启动 | 会话结束 | 进度、待办、提醒 |
| task-log.md | 按需 | 任务状态变化 | 任务档案 |
| wechat-memory.jsonl | 按需检索 | 值得记时 | 微信重要记忆 |
| user-profile.md | 每次启动 | 发现新偏好 | 用户偏好 |

### Claude 区（8 个文件）

| 文件 | 加载时机 | 更新时机 | 内容 |
|------|----------|----------|------|
| MEMORY_INDEX.md | CODE启动加载 | 文件变化时 | 全局记忆地图 |
| code-claude-framework.md | 按需 | 框架变化时 | 协作框架 |
| data-source-log.md | 按需 | 每次数据拉取 | 接口状态 |
| task-result-cache.md | 按需 | 每次任务完成 | 结果存根 |
| user-profile.md | 每次启动 | 发现新偏好 | 用户偏好 |
| trading-agent-project-framework.md | 按需 | 项目变化 | QPSM项目 |
| kline_patterns.md | 按需 | 规则更新 | K线形态 |
| deepseek_preference.md | 按需 | 配置变化 | DS API |
| mobile_frontend.md | 按需 | 配置变化 | 手机前端 |

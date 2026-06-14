# CODE × Claude 架构文档

## 一、角色分工

| 维度 | CODE | Claude |
|------|------|--------|
| 定位 | 传输审核层 | 数据落实层 |
| 入口 | 微信 | 服务器终端 |
| 职责 | 理解意图、拆任务单、审核结果、推微信 | 拉数据、跑计算、写代码、出结果 |
| 不负责 | 写代码、跑数据、架构设计 | 微信对话、用户交互 |
| 模型 | Claude API（桥接） | DeepSeek / Claude |

## 二、记忆三层隔离

### 记忆目录树

```
~/.claude/projects/
├── -home-ubuntu-xiaoke/memory/      ← CODE 区（传输审核层）
│   ├── role-guard.md                🔒 角色锁
│   ├── session-handoff.md           ✏️ CODE
│   ├── task-log.md                  ✏️ CODE
│   ├── wechat-memory.jsonl          ✏️ CODE（高频）
│   └── user-profile.md              ✏️ 双方
│
├── -home-ubuntu/memory/             ← Claude 区（数据落实层）
│   ├── MEMORY_INDEX.md              🔒 全局记忆地图
│   ├── code-claude-framework.md     🔒 协作框架
│   ├── data-source-log.md           ✏️ Claude
│   ├── task-result-cache.md         ✏️ Claude
│   ├── user-profile.md              ✏️ 双方
│   ├── trading-agent-project-framework.md
│   ├── kline_patterns.md
│   ├── deepseek_preference.md
│   └── mobile_frontend.md
│
└── -home-ubuntu-trading-agent/memory/ ← Trading 区
    └── ...
```

### 权限矩阵

| | CODE 写 | Claude 写 | CODE 读 | Claude 读 |
|------|:---:|:---:|:---:|:---:|
| CODE 区 | ✏️ | ✗ | 👁 | 👁 |
| Claude 区 | ✗ | ✏️ | 👁 | 👁 |
| Trading 区 | ✗ | ✏️ | 👁 | 👁 |
| user-profile.md | ✏️ | ✏️ | 👁 | 👁 |

## 三、CODE 上下文策略

```
会话启动自动加载：
  1. MEMORY_INDEX.md（知道所有记忆在哪）
  2. role-guard.md（角色锁）
  3. session-handoff.md（上次聊到哪）
  4. user-profile.md（用户是谁）
  5. 前 30 轮对话（上下文窗口，不进文件）

按需检索：
  搜对应文件关键词

对话结束：
  更新 session-handoff.md
  追加 wechat-memory.jsonl
```

## 四、一致性审计

### 核验逻辑

```
返回结果中多指标交叉验证：
  方向一致的指标 ≥ 多数 → ✅ 可信
  方向打架的指标 ≥ 2 组  → ❌ 打回，附具体矛盾点
```

### 审核清单（CODE 每次核验）

| # | 检查项 | 方法 |
|---|--------|------|
| 1 | 数据来源声明 | 每条结果有没有标注来源 |
| 2 | 时间戳 | 每条数据有没有拉取时间 |
| 3 | 缺失声明 | 缺了什么、为什么、怎么替代 |
| 4 | 方向一致性 | 价格 + 量 + 指标方向是否一致 |
| 5 | 自洽性 | 总和、数量、正负是否合理 |
| 6 | 子步骤衔接 | 上一步输出是否出现在下一步输入 |

## 五、心跳监控

| 触发 | 时间 | 动作 |
|------|------|------|
| 任务发出 | 0s | CODE 回复"处理中"，开始计时 |
| 一级提醒 | 5 分钟 | CODE 推微信"数据还在跑，稍等" |
| 二级兜底 | 15 分钟 | CODE 自己拉数据 → 审核 → 推微信 + 免责 |

## 六、返回结果元数据标准

每次 Claude/DeepSeek 返回必须带：

| 字段 | 必填 | 说明 |
|------|:--:|------|
| 数据来源 | ✅ | 接口 URL / 库名 / 文件名 |
| 拉取时间戳 | ✅ | 每条数据的实际获取时间 |
| 缺失字段 | ✅ | 字段名 + 原因 |
| 替代方案 | ✅ | 换了什么备源 / 用什么填充 |
| 计算结果 | ✅ | 信号值、指标值、形态判定 |

## 七、冲突处理

```
CODE 先到（15分钟自拉）→ Claude 后到（复核结果）：
  1. CODE 结果先推，附免责
  2. Claude 结果后推，附"复核结果"
  3. 不一致处 CODE 标出
  4. 以 Claude 复核为准
```

## 八、硬规则

1. CODE 不写 Claude 区，Claude 不写 CODE 区
2. 任务单必须含 verification_rules
3. 返回必须含数据来源+时间戳+缺失说明
4. 用户说"记一下"：立即写 wechat-memory.jsonl
5. CODE 不加载全局 CLAUDE.md，角色锁覆盖

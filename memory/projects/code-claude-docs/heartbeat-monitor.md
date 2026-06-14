# 心跳监控与兜底机制

## 监控时序

```
任务发出 → pending
  │
  ├── 0s   → CODE 回复"处理中"，开始计时
  ├── 300s → CODE 推微信"还在跑，稍等"
  ├── 900s → CODE 自己拉数据 → 审核 → 推微信
  └── 任意 → Claude 回结果了 → 审核 → 正常流程
```

## 实现方式

bridge.py 后台 watchdog 线程，每 60 秒扫一次 task 目录。

### 检查逻辑

```
扫 tasks/task_*.json：
  跳过 result_ 文件
  只查 status=pending 的任务
  计算 elapsed = now - created_at
    elapsed > 900s 且未 poke → 触发二级兜底
    elapsed > 300s 且未 nudge → 触发一级提醒
```

## CODE 兜底拉数据

### 触发条件

1. 任务 pending 超过 15 分钟
2. 同一任务打回 ≥ 3 次
3. 用户主动说"你自己查"

### 执行方式

bridge 调 `code_data_fallback.py` 独立拉数据（不经过 Claude）

### 回复模板

```
"等了15分钟Claude那边没反应，我自己去查了。

[数据结果]

⚠️ 以上是我直接从[数据源]拉的数据，没经过Claude复核。
参考用，确认后让Claude再跑一次。"
```

## 两级提醒模板

### 一级（5 分钟）

```
NUDGE: "数据那边还在跑，再等等。"
```

### 二级（15 分钟）

```
POKE: "Claude 15 分钟没回——可能挂了/卡了/接口崩了。
我现在自己查，等我会。"
```

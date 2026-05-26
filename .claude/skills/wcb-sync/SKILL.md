---
name: wcb-sync
description: |
  从 WCB Agent API 自动拉取每日任务和事件，落到对应日期的 TASK.md。当用户说"拉一下今天任务"、"wcb sync"、"同步任务"、"看看今天有什么活动"时触发。适用于 web3career-study-track 项目的每日任务收集流程。免去手动从 web3career.build 页面复制任务的步骤。
---

# WCB Sync Skill

通过 WCB Agent API 一键拉取指定日期的事件和任务，自动落到对应 daily-log 的 TASK.md。

## 触发场景

- 用户说"拉一下今天的任务"
- 用户说"wcb sync"或"`/wcb-sync`"
- 用户说"同步今天的任务"、"看今天有什么活动"
- 用户说"拉一下 5/24 的任务"（可指定日期）
- 一天开始前需要确认当日 WCB 任务

## 前置条件

**密钥**：用户的 WCB Agent API Secret Key 必须配置在 User 级环境变量 `WCB_AGENT_SECRET_API_KEY`。

验证：
```powershell
Test-Path env:WCB_AGENT_SECRET_API_KEY
$env:WCB_AGENT_SECRET_API_KEY.Substring(0, 12)  # 应输出 "w3cb_sk_..."
```

如果密钥未配置，提示用户：
```
密钥未配置。请运行：
[System.Environment]::SetEnvironmentVariable("WCB_AGENT_SECRET_API_KEY", "<your_key>", "User")
然后重启终端或新会话。
```

## API 入口

- Base URL: `https://web3career.build`
- 调用端点: `POST /api/agent/call`
- 文档: `https://web3career.build/llms.txt`
- 当前用户 programId: `cmnx791nl008sru0167pzp4ki`（AI x Web3 School）

## 工作流程

### Step 1 · 解析日期参数

- 无参数 → 今天（系统日期）
- `/wcb-sync 5/24` 或 `/wcb-sync 2026-05-24` → 解析为 ISO 8601 范围
- 时区：默认 `Asia/Shanghai` (UTC+8)，转换为 UTC 时拉宽一日范围
- 范围：`YYYY-MM-DDT00:00:00.000Z` 到 `YYYY-MM-DDT24:00:00.000Z`（次日 0 点）

### Step 2 · 拉取当日 events

```powershell
$headers = @{ "Authorization" = "Bearer $env:WCB_AGENT_SECRET_API_KEY"; "Content-Type" = "application/json" }
$body = @{
  procedure = "events.listForLearner"
  input = @{
    programId = "cmnx791nl008sru0167pzp4ki"
    rangeStart = "<ISO start>"
    rangeEnd = "<ISO end>"
  }
} | ConvertTo-Json -Depth 3
$events = Invoke-RestMethod -Method POST -Uri "https://web3career.build/api/agent/call" -Headers $headers -Body $body
```

每个 event 含：`title`、`description`、`startAt`、`endAt`、`meetingUrlPrimary`、`replayUrl`、`taskIds[]`。

### Step 3 · 拉取关联 tasks

收集所有 events 的 `taskIds`，去重，批量查询：

```powershell
$body = @{
  procedure = "tasks.listForLearnerByIds"
  input = @{
    programId = "cmnx791nl008sru0167pzp4ki"
    taskIds = $allTaskIds
  }
} | ConvertTo-Json -Depth 3
$tasks = Invoke-RestMethod -Method POST -Uri "https://web3career.build/api/agent/call" -Headers $headers -Body $body
```

每个 task 含：`title`、`description`、`points`、`status`、`validTo`、`exclusiveGroupKey`、`proofPrompt`。

### Step 4 · 生成 TASK.md 内容

按以下模板组装内容，写到 `daily-log/week-N/YYYY-MM-DD/TASK.md`（如已存在，与现有内容 merge）：

```markdown
# YYYY-MM-DD 任务

> 自动拉取自 WCB Agent API · 拉取时间 <YYYY-MM-DD HH:mm UTC+8>

## 今日任务清单

| # | 任务 | 时间 | 学分 | 状态 |
|---|------|------|------|------|
| 1 | <task title> | <event start time HH:mm> | +<points> | ⚪ 未开始 |

> 状态图例：⚪ 未开始 · ⏳ 进行中 · ✅ 已完成 · ❌ 错过 · 📤 已提交

## 任务详情

### 任务 #N · <task title>

- **学分**：+<points>
- **截止**：<validTo 转 Asia/Shanghai>
- **互斥组**：<exclusiveGroupKey>（若多个任务同组，仅可领其一）
- **会议链接**：<meetingUrlPrimary>
- **直播回放**：<replayUrl>
- **提交要求**：<proofPrompt>

#### 课前准备

<from event description if relevant>

#### 产出（手填）

- [ ]

#### 交付证明（手填）

>
```

### Step 5 · 写入与提示

**写入策略：**

- 如果 TASK.md 不存在（仅有模板）→ 直接写入
- 如果 TASK.md 已有手填内容（产出 / 交付证明非空）→ 仅在文件顶部更新「今日任务清单」表格 + 任务详情元数据，不覆盖手填内容
- 如果不确定 → 先展示 diff 让用户确认

**写入后：**

输出汇总：
```
✓ 拉取到 N 个 event / M 个 task
✓ 写入 daily-log/week-N/YYYY-MM-DD/TASK.md
TODO: 任务完成后回填「产出」和「交付证明」，并到 WCB 平台手动提交
```

## 互斥组提示

WCB 经常有"实时参加 / 观看回放"互斥设计（同一直播两个任务，二选一）。检测到 `exclusiveGroupKey` 重复时：

- 在表格状态列加备注 `（与 #X 互斥）`
- 在任务详情节强调

## 边界与限制

- **不自动提交任务**：本 skill 只拉取，不写入。提交 evidence 必须用户手动到 WCB 平台或显式调用 `tasks.submitEvidence`（需用户授权）
- **不动手填内容**：用户已经在 TASK.md 写的产出 / 反思一律保留
- **密钥不入版本**：永远不要把 API key 写入 commit message、TASK.md 或任何被 git track 的文件
- **编码注意**：Windows PowerShell 默认 GBK 显示，写文件时确保 UTF-8 编码（用 `Out-File -Encoding utf8` 或直接 Write 工具）

## 与其他规范的关系

- 任务结构遵循 [`GUIDE.md`](../../../GUIDE.md) "任务清单生成流程"节
- 周级任务清单沉淀仍在 `week-N/__index__.md`，本 skill 只填日级 TASK.md
- 完成后的 commit 走 [`git-commit-guide`](../git-commit-guide/SKILL.md)（type 用 `task`）

## 示例调用

```
用户：拉一下今天的任务
Agent：
  1. 检测今天 = 2026-05-23
  2. 调用 events.listForLearner，得到 1 个 event："Open Agentic Economy"
  3. 调用 tasks.listForLearnerByIds，得到 2 个 task（实时 +20 / 回放 +10，互斥）
  4. 写入 daily-log/week-1/2026-05-23/TASK.md
  5. 输出汇总 + 提示用户去 WCB 平台提交
```

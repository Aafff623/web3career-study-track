---
name: daily-log-sync
description: |
  一天学习结束后，同步 daily-log、更新状态、按模块分组 commit & push。当用户说"写一下今天的 daily-log"、"同步一下今天的日志"、"commit 一下"时触发。适用于 web3career-study-track 项目的每日收尾流程。
---

# Daily Log Sync Skill

一天学习结束后的收尾流程：整理日志、更新状态、分组提交。

## 触发场景

- 用户说"写 daily-log"
- 用户说"今天的东西 commit 一下"
- 用户说"同步日志"
- 一天学习结束，需要整理当日记录

## 工作流程

### 1. 确认当日完成情况

读取当日 TASK.md（如有），确认任务完成状态。如果没有 TASK.md，从 git log 和文件变更推断当日工作。

### 2. 更新 YYYY-MM-DD.md

在 `daily-log/week-N/YYYY-MM-DD/YYYY-MM-DD.md` 中记录：

```markdown
# YYYY-MM-DD 学习日志

## 今日完成
- [简要描述完成的工作，链接到具体产出]

## 产出与检验
| 产出 | 状态 | 链接 |
|------|------|------|
| xxx | ✅ 已完成 | [链接](./path) |

## 收获 / 卡点
- 真实感受，不写流水账
- 卡住的地方写清楚卡在哪、怎么解决的

## 明日打算
- 具体的下一步
```

**关键约束：**
- 产出表用链接引用，不重复展开内容
- 收获写真实感受，不写流水账

### 3. 更新 __index__.md

更新 `daily-log/week-N/YYYY-MM-DD/__index__.md` 中的状态标记。

### 4. 按模块分组 commit

遵循 commit 规范 `<type>(<scope>): <subject>`，按产出类型分组：

| type | scope | 说明 |
|------|-------|------|
| `study` | 模块名 | 预习笔记、实践文件 |
| `task` | 任务编号 | TASK.md 中的任务产出 |
| `log` | week-N | 日志文件 |
| `docs` | 通用 | README、规范文件、memory |

**每个模块一个 commit**，不合并多个模块到一个 commit。

### 5. Push

等待用户 review 后，确认 push。

## 约束

- commit message 用中文，简洁准确
- 不要合并多天的改动到一个 commit
- 日志中的"收获"部分要写真实想法，不要泛泛而谈
- 不要自动 commit & push，完成任务后等用户确认

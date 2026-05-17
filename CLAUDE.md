# CLAUDE.md

> 项目级 AI 助手指令文件，适用于 Claude Code / Kiro / 类似工具

## 项目概述

这是 AI Web3 School BootCamp（4 周共学营 + 黑客松）的学习记录仓库。内容包括每日笔记、任务打卡、预习资料和 Hackathon 项目代码。

## 仓库结构

- `daily-log/YYYY-MM-DD/` — 每日学习记录（笔记 + 任务 + 资源）
- `pre_study/` — 预习阶段 42 节知识笔记
- `hackathon/` — Hackathon 项目代码与演示
- `reference/` — 规范文件

## 工作约定

### 文件操作

- 每日记录放 `daily-log/对应日期/` 下，不要跨天合并
- 笔记写在 `YYYY-MM-DD.md`，任务写在 `TASK.md`，索引和链接写在 `__index__.md`
- 图片放 `assets/` 文件夹，用相对路径引用
- 预习笔记按模块放对应子文件夹，每个主题一个文件夹

### Git 提交

- 遵循 `reference/git-commit-reference.md` 中的规范
- 格式：`<type>(<scope>): <subject>`
- 高频类型：`log`（笔记）、`task`（任务打卡）
- scope 用 `MM-DD` 日期格式
- 不合并多天内容为一个 commit

### 内容风格

- 中文为主，技术术语保留英文
- 笔记结构：概览 → 关键收获 → 问题与讨论
- 保持简洁，避免完美主义，先记录再优化

### Hackathon 阶段（Week 3-4）

- 合约代码放 `hackathon/contracts/`
- Demo 材料放 `hackathon/demo/`
- 部署后在 TASK.md 中记录 Tx Hash 和合约地址
- commit 类型用 `feat` / `contract` / `fix`

## 禁止事项

- 不要修改 `reference/` 下的规范文件（除非明确要求）
- 不要在 commit message 中暴露私钥、助记词等敏感信息
- 不要把 `.env` 或密钥文件加入版本控制

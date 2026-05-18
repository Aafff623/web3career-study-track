---
name: guide-md-restructure
description: 规范文件重构为三层架构（GUIDE.md + CLAUDE.md + steering.md），两个工具文件保持内容对齐
metadata:
  type: project
---

2026-05-18 完成规范文件体系重构，从 CLAUDE.md 大杂烩拆分为三层架构：

- **GUIDE.md**：公共规范（仓库结构、文件操作、Git 规则、任务流程、内容风格、Hackathon 阶段、禁止事项）
- **CLAUDE.md**：Claude Code 专用（引用 GUIDE.md + 目标/阶段/决策/方向 + 行为约定）
- **steering.md**：Kiro 专用（引用 GUIDE.md + 目标/阶段/决策/方向 + 行为约定）

**Why:** 用户同时使用 Claude Code 和 Kiro 交替管理项目，之前两个文件内容不同步，存在规范一致性问题。

**How to apply:** 以后修改项目规范时，公共内容改 GUIDE.md，个性化内容在 CLAUDE.md 和 steering.md 中同步更新。两个文件的主体结构应保持一致，只在行为约定节名上有差异。

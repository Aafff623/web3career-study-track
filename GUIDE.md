# GUIDE.md

> 项目通用规范与工作索引 —— 无论用 Claude Code、Kiro 还是其他 AI 编程工具接入本项目，均以此文件为准。

## 项目概述

这是 AI Web3 School BootCamp（4 周共学营 + 黑客松）的学习记录仓库。内容包括每日笔记、任务打卡、预习资料和 Hackathon 项目代码。

## 仓库结构

- `daily-log/week-N/YYYY-MM-DD/` — 每日学习记录（笔记 + 任务 + 资源）；按周→日两层组织
- `daily-log/week-N/WEEK.md` — 当周完整目标、任务和推荐材料
- `daily-log/week-N/__index__.md` — 当周概览与每日索引
- `pre_study/` — 预习阶段 42 节知识笔记
- `hackathon/` — Hackathon 项目代码与演示
- `reference/` — 规范文件

## 工作索引规范

### 文件操作

- 每日记录放 `daily-log/week-N/对应日期/` 下，不要跨天合并
- 笔记写在 `YYYY-MM-DD.md`，任务写在 `TASK.md`，索引和链接写在 `__index__.md`
- 周级目标和任务写在 `daily-log/week-N/WEEK.md`，周级索引写在 `daily-log/week-N/__index__.md`
- 图片放 `assets/` 文件夹，用相对路径引用
- 预习笔记按模块放对应子文件夹，每个主题一个文件夹
- 预习笔记中的"最小实践"练习，抽成独立文件放在同级目录，文件名用英文（如 `transaction-explainer.md`），与 `README.md` 平级
- 预习笔记排版：每个 `###` 子标题之间留 2 行空行，避免内容过于紧凑

### 预习笔记批注规范

- 格式：使用 blockquote + 斜体，即 `> *批注内容*`
- 位置：紧跟在对应段落之后，不另起章节
- 风格：精炼技术总结，用自己的话复述核心要点，像给未来的自己写备忘
- 不写：个人情绪故事、比喻段落、"我觉得好酷"类感叹
- 要写：本质是什么、要记住什么、在 AI×Web3 场景里意味着什么
- 行动导向：涉及应对措施时，用编号列表直接列出

### Git 提交

- 遵循 `reference/git-commit-reference.md` 中的规范
- 格式：`<type>(<scope>): <subject>`
- 高频类型：`log`（笔记）、`task`（任务打卡）
- scope 用 `MM-DD` 日期格式
- 不合并多天内容为一个 commit, 每一阶段完成的内容进行细致化的 git 分类

### 任务清单生成流程

> 把任务平台 / 主办方页面上看到的任务信息，结构化地落到对应文件里。

**输入**（由人提供）：
- **当日上下文**：当天面板上的具体任务（线上活动、Co-learning、相关链接、学分、截止）
- **当周上下文**：整周任务总览（前置准备、AI 向、Web3 向、综合、行业观察等长期任务）

由用户进行提供 和 补充原始的参考来源

**输出位置**：

- **当日具体任务（线上活动 / 当天的提交）** → `daily-log/week-N/YYYY-MM-DD/TASK.md`
- **整周任务菜单（长期任务 + 全周日期事件）** → `daily-log/week-N/__index__.md` 的 "本周课程任务清单" 节
- **任务对应的知识沉淀** → `pre_study/<module>/<topic>/README.md`
- **当日的执行叙事和反思** → `daily-log/week-N/YYYY-MM-DD/YYYY-MM-DD.md`

**TASK.md 写法**：

- 顶部 "今日任务清单" 表格列出当天所有任务（# / 任务 / 时间 / 学分 / 状态）
- 状态图例：⚪ 未开始 · ⏳ 进行中 · ✅ 已完成 · ❌ 错过 · 📤 已提交
- 每个任务展开 "任务详情" 子节，含会议链接 / 课前准备 / 注意事项
- 完成后回填 "产出" 和 "交付证明"
- 详细叙事不在 TASK.md 里写，写到当日 `YYYY-MM-DD.md`，TASK.md 只链过去

**周任务清单写法**（在 `week-N/__index__.md` 里）：
- 按类别分表：前置准备 / 实时参加 / 回放兜底 / AI 向 / Web3 向 / 综合 / 总结观察
- 每行：状态 + 日期（如有） + 任务 + 学分
- 末尾给学分汇总（上限值，不含互斥）

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
- 不要在完成用户任务之后直接 commit & push, 需要经过用户的Review之后的授权示意
- 后续如果有黑客松的项目, 不要把 `.env` 或密钥文件加入版本控制

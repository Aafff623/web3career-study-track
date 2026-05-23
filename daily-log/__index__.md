# daily-log 规范

> 按 **周 → 日** 两层组织：每周一个 `week-N/` 文件夹包含本周目标和 7-8 天的日记录。

## 目录结构

```
daily-log/
├── __index__.md              ← 本文件（规范 + 模板）
├── week-1/                   ← Week 1: 2026-05-17 — 2026-05-23
│   ├── __index__.md           当周概览 + 每日索引表
│   ├── WEEK.md                当周完整目标、任务、推荐材料、交付清单
│   ├── 2026-05-17/
│   ├── ...
│   └── 2026-05-23/
├── week-2/                   ← Week 2: 2026-05-24 — 2026-05-30
├── week-3/                   ← Week 3: 2026-05-31 — 2026-06-06
└── week-4/                   ← Week 4: 2026-06-07 — 2026-06-14
```

## 周级文件（`week-N/` 下）

| 文件 | 用途 |
|------|------|
| `__index__.md` | 当周概览：主题、状态、每日索引表、交付清单 |
| `WEEK.md` | 当周完整内容：学习目标、模块结构、推荐材料、实践任务、交付要求 |

## 日级文件（`week-N/YYYY-MM-DD/` 下）

| 文件 | 用途 |
|------|------|
| `__index__.md` | 当日索引：概览、参考链接、资料汇总 |
| `YYYY-MM-DD.md` | 当日学习笔记（课程内容、Co-Learning 讨论、问答记录） |
| `TASK.md` | 当日任务与产出（打卡内容、交付证明、Tx Hash） |
| `meetings/` | 直播 / Co-Learning / Workshop 录播笔记（按场次拆分，slug 命名）— 仅当日有直播时建。约定详见 [`GUIDE.md`](../GUIDE.md) 的"直播录播笔记规范"节 |
| `assets/` | 截图、图片等静态资源 |

---

## 模板：周级 `__index__.md`

```markdown
# Week N ｜ <主题>

> YYYY-MM-DD — YYYY-MM-DD

## 本周概览

- 主题：
- 完整目标 / 任务：[`WEEK.md`](./WEEK.md)
- 状态：未开始 ⚪ / 进行中 🟢 / 已完成 ✅

## 每日索引

| 日期 | 主题 / 活动 | 笔记 | 任务 |
|------|-------------|------|------|
| YYYY-MM-DD (周X) | — | [📝](./YYYY-MM-DD/YYYY-MM-DD.md) | [⏳](./YYYY-MM-DD/TASK.md) |

## 本周交付清单

- [ ] ...
```

## 模板：周级 `WEEK.md`

```markdown
# Week N ｜ <完整标题>

> **周期**：YYYY-MM-DD — YYYY-MM-DD
> **主题**：

## 本周学习目标

## 模块结构

## 推荐材料 / 参考入口

## 实践任务 / 挑战

## 本周交付
```

## 模板：日级 `__index__.md`

```markdown
# YYYY-MM-DD

> Week N · Day X · 周X

## 今日概览

- 主题 / 活动：
- 状态：⚪ 未开始 / 🟢 进行中 / ✅ 已完成
  - [ ] 笔记 → [`YYYY-MM-DD.md`](./YYYY-MM-DD.md)
  - [ ] 任务 → [`TASK.md`](./TASK.md)

## 当日文件

| 文件 | 内容 |
|------|------|
| [`YYYY-MM-DD.md`](./YYYY-MM-DD.md) | 当日笔记：做了什么、产出与检验、收获与卡点 |
| [`TASK.md`](./TASK.md) | 任务描述、截图、交付证明 |
| [`meetings/<slug>.md`](./meetings/) | 直播录播笔记（当日有直播时）|
| [`assets/`](./assets/) | 截图、图片资源 |

## 关联引用

> 今天涉及到的预习笔记或上下文，链接放这里，正文不重复展开。

- 预习笔记：

## 参考链接

-

## 备注

-
```

## 模板：日级 `YYYY-MM-DD.md`

```markdown
# YYYY-MM-DD

> Week N · Day X · 周X

## 今天做了什么

-

## 产出与检验

> 实际产出（笔记 / 代码 / 截图 / Tx Hash / commit）+ 怎么证明做完了。
> 涉及的预习概念直接引用 `pre_study/.../README.md`，不在这里重复展开。

## 收获 / 卡点

> 今天真实的感受：学到什么、卡在哪、想到什么疑问。一两条就够。

## 明天打算

> 短短一行。
```

## 模板：日级 `TASK.md`

```markdown
# YYYY-MM-DD 任务

## 任务来源

- 平台：WCB / Co-Learning / 其他
- 学分：
- 截止：

## 任务描述

> 官方任务说明（截图或粘贴文字）。

## 产出

> 实际交付的东西，列要点即可。详细叙述放 `YYYY-MM-DD.md`。

## 交付证明

> 截图 / 链接 / Tx Hash / commit hash

![](./assets/)
```

---

## 维护节奏

- **每天**：在对应 `week-N/YYYY-MM-DD/` 下更新 `YYYY-MM-DD.md` 和 `TASK.md`，并维护当日 `__index__.md`。
- **每周开始**：在对应 `week-N/__index__.md` 标记状态为 🟢 进行中，并补充 `WEEK.md` 详情（如主办方已公布）。
- **每周结束**：把 `week-N/__index__.md` 标记为 ✅ 已完成，回顾交付清单完成度。
- **commit 规范**：见 [`reference/git-commit-reference.md`](../reference/git-commit-reference.md)。

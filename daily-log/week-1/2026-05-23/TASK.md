# 2026-05-23 任务

> 自动拉取自 WCB Agent API · 拉取时间 2026-05-23 · 通过 `/wcb-sync` 同步

## 今日任务清单

| # | 任务 | 时间 | 学分 | 状态 |
|---|------|------|------|------|
| 1 | 实时参加｜Open Agentic Economy: From ERC-8004 / ERC-8183 to Builder Path | 09:30 - 10:30 | +20 | ✅ 已完成 |
| 2 | 观看回放｜Open Agentic Economy（与 #1 互斥，不重复领） | 同上 | +10 | ❌ N/A（已实时参加）|

> 状态图例：⚪ 未开始 · ⏳ 进行中 · ✅ 已完成 · ❌ 错过 · 📤 已提交

## 任务详情

### 1. Open Agentic Economy: From ERC-8004 / ERC-8183 to Builder Path

- **时间**：2026-05-23 09:30 - 10:30（Asia/Shanghai）
- **主讲**：Sophia（Ethereum Foundation Developer Acceleration Team）
- **适合对象**：对 Agentic Economy、机器支付、协议标准和 Builder 路径感兴趣的学员
- **你会学到**：ERC-8004 / ERC-8183 等方向如何连接 Agent、支付、身份、验证和应用构建路径，以及这些标准对 AI × Web3 项目设计的启发
- **课前准备**：提前准备一个你对 Agent 经济、机器支付或链上验证的疑问
- **关联任务**：
  - Week 1｜线上活动｜实时参加 5.23｜Open Agentic Economy（+20 学分）✅
  - Week 1｜线上活动｜观看回放 5.23｜Open Agentic Economy（+10 学分，与实时参加互斥，不重复领）
- **互斥组**：`week1-0523-open-agentic-economy`
- **提交截止**：2026-05-24 23:59:59（Asia/Shanghai）

#### 会议链接

- Zoom：<https://us06web.zoom.us/j/85095506116?pwd=ueJDJR10WC52l2sfH329YitKaFtCMb.1>
- 会议号：850 9550 6116 · 密码：175525
- X 直播 / 回放：<https://x.com/i/broadcasts/1qxvvkQkVXQxB>

#### 提交要求

提交实时参与截图，并补充 1 条从本场活动中获得的关键信息、问题或下一步行动。**不要提交私钥 / 助记词 / API Key 或其他敏感信息。**

## 产出

> 实际交付的东西，列要点即可。详细叙述放 [`2026-05-23.md`](./2026-05-23.md)。

**直播参与**

- Open Agentic Economy 实时参加完成（09:30-10:30）
- 直播笔记入库：[`meetings/open-agentic-economy.md`](./meetings/open-agentic-economy.md)（biliGPT 清洗版 + 4 个章节截图）

**仓库基建**

- 新建 [`toolkit/`](../../../toolkit/) 工具箱模块（`tools/` + `workflows/` 两分区 + 总览 README）
- 沉淀 [`livestream-note-pipeline.md`](../../../toolkit/workflows/livestream-note-pipeline.md) 直播录播笔记完整工作流
- [`GUIDE.md`](../../../GUIDE.md) 新增"直播录播笔记规范"节
- [`CLAUDE.md`](../../../CLAUDE.md) / [`steering.md`](../../../steering.md) 决策记录补 05-22（extras）+ 05-23（toolkit）

**直播笔记全量回补（Week 1）**

| 日期 | 笔记文件 | 来源 |
|------|---------|------|
| 5/17 | `meetings/opening-ceremony.md` | biliGPT |
| 5/18 | `meetings/ai-web3-basics.md` · `meetings/go-learning.md` | biliGPT 替换 + 旧迁移 |
| 5/19 | `meetings/hermes-from-zero.md` | biliGPT |
| 5/20 | `meetings/web3-fundamentals.md` · `meetings/co-learning.md` | biliGPT · 占位 |
| 5/21 | `meetings/agent-24h-workflow.md` | biliGPT |
| 5/22 | `meetings/co-learning.md` · `meetings/week1-recap.md` | 占位 ×2 |
| 5/23 | `meetings/open-agentic-economy.md` | biliGPT |

**WCB Agent API 接通**

- API 密钥配置到 User 级环境变量 `WCB_AGENT_SECRET_API_KEY`
- 测通 5 个接口：`health.check` / `users.getProfile` / `events.listForLearner` / `tasks.listForLearnerByIds` / `users.getMyPermissions`
- 沉淀 [`/wcb-sync` skill](../../../.claude/skills/wcb-sync/SKILL.md)，本次 TASK.md 就是用它生成的

**extras/ 加餐**

- 新增 [`extras/web3/17h-web3-course/`](../../../extras/web3/17h-web3-course/) — B 站 17 小时 Web3 教程系列 5 课笔记（biliGPT 清洗，5 个 parallel agent 调度完成）
- 入库内容：02 Solidity Hello World / 03 FundMe & ERC-20 / 05 Hardhat 测试 / 06 CCIP 跨链 / 07 接下来做什么
- 系列 README 含课程结构图 + 学习记录

**索引校正与 cascade 同步**

- [`README.md`](../../../README.md) cascade：目录树补 `toolkit/` + `meetings/` · Highlights skill 数 3→4 · 5/23 进度行 · 最后更新日期
- [`week-1/__index__.md`](../__index__.md) 实时参加状态：5/19/20/21/23 标 ✅ + 删 5/23 Co-learning 空挡 + 学分汇总微调
- [`daily-log/__index__.md`](../../__index__.md) 日级模板补 `meetings/` 行

## 交付证明

> 截图 / 链接 / Tx Hash / commit hash

**直播参与**

- 截图待补充到 `./assets/`
- 1 条关键信息：**ERC-8004 的 reputation 是给 Agent 本身的，不是给背后的 owner —— 这点决定了 Agent 在机器经济中可以作为独立主体被筛选 / 组合 / 调用**

**今日已 commit（10 个，本地领先 origin/master）**

```
2e28d78 docs(readme): cascade 同步 — toolkit 入口 + meetings 子目录 + 5/23 进度行 + skill 数 3→4
bec79ad chore(week-1): 索引校正 — 5/19/20/21/23 实时直播标 ✅ + 删 5/23 Co-learning 空挡 + 学分汇总微调
824165d log(05-23): Open Agentic Economy 直播笔记 — Sophia · ERC-8004 / CROPS / Builder Path
e89b8e3 log(05-22): Co-learning + Week 1 例会占位笔记 — 元数据 + 简短叙事
ec5d929 log(05-21): AI 下乡直播笔记 — Sunny · 24h Agent 工作流 + Claude/Codex 协作
0a10d4c log(05-20): Web3 运行原理直播笔记 — BRUCE · 交易生命周期 + Co-learning 占位
ada2d7a log(05-19): Hermes 从 0 到 1 直播笔记 — Dra 老师 · Agent 五大阵营 + WSL 部署
8e1e7d2 log(05-17): 开营仪式直播笔记 — ZAI / GLM 5.1 / Hermes 配置 + CROPS 学习方法论
bc52e89 log(05-18): biliGPT 完整版替换 ai-web3-basics 手写简版 — 同主题但内容更结构化
ce397ac chore(toolkit): 新建工具箱 + 直播录播笔记工作流 — biliGPT 沉淀路径标准化
```

**待 commit（已 review pass）**

- `extras/web3/17h-web3-course/` 5 课笔记 + 系列 README + extras/web3/README.md 更新
- `daily-log/week-1/2026-05-23/meetings/open-agentic-economy.md` 补 4 个章节截图
- `daily-log/week-1/2026-05-23/__index__.md` + 本 TASK.md
- `.claude/skills/wcb-sync/SKILL.md` 新建

**WCB 平台手动提交（待办）**

- [ ] 到 [WCB Learning](https://web3career.build/zh/programs/AI-Web3-School#tab=learning) 提交 Open Agentic Economy 实时参与 proof（截图 + 1 条关键信息）→ 截止 5/24 23:59

![](./assets/)

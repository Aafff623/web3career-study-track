# AI Web3 School · 我的共学营笔记本

> 4 周线上共学营 + 黑客松，主题是 AI × Web3 交叉方向。
> 开营：2026-05-17 · 状态：进行中 🟢

## 这是什么

这个仓库是我参加 [AI Web3 School BootCamp](https://aiweb3.school/) 的"工作台"——从开营那天到 Hackathon 提交，所有的课程笔记、Co-Learning 讨论、每日打卡、踩过的坑、最后那个能跑起来（希望能跑起来）的项目，都堆在这里。

不是写给别人看的展示稿，更像是我自己的实验记录簿，顺便公开。

## 为什么是这件事

最近一直在想一个问题：

> 当 AI Agent 真的能调用工具、读写数据、甚至触发支付的时候，**谁授权？谁付款？责任边界在哪？**

我越想越觉得，这不是 AI 圈子单方面能回答的问题。授权、签名、不可伪造的执行记录、可撤销的能力——这些恰好是 Web3 这十年攒下来的基础设施在做的事。

但两边的人现在还各说各话：AI 圈子里很多人不知道 Session Key 是啥，Web3 圈子里很多人觉得 Agent 只是"接个 API 而已"。我想花这 4 周泡在这个交叉地带，把两套语言学到能互译，最后做出一个能在测试网上跑起来的小东西。

这个仓库就是这个过程。

## 整体节奏

| 阶段 | 时间窗口 | 我在干啥 | 想交付的东西 |
|------|---------|---------|------------|
| Week 1 | 05/17 — 05/23 | 把 AI 和 Web3 的基础概念串到一条线上 | 基础笔记 + Co-Learning 打卡 |
| Week 2 | 05/24 — 05/30 | 钻进 AI × Web3 真正交叉的那些点 | Bridge 模块笔记 + 分享会记录 |
| Week 3 | 05/31 — 06/06 | 选定 Hackathon 方向，开始动手 | 项目方向定稿 + 第一版能跑的代码 |
| Week 4 | 06/07 — 06/14 | 闷头开发、改 bug、交东西 | 最终代码 + 测试网 Tx Hash + Demo |

每天的循环大致是：**听课/分享会 → Co-Learning 讨论 → 当日任务 → 写笔记 → commit**。

## 仓库怎么组织

我把仓库刻意做成了"输入 → 过程 → 输出"三层：

```
web3career-study-track/
│
├── README.md                  ← 你正在看的这个
├── GUIDE.md                   ← 项目通用规范（Claude Code / Kiro 等工具共用）
├── CLAUDE.md                  ← Claude Code 专用行为指引
├── steering.md                ← Kiro 专用方向与决策指引
│
├── pre_study/                 ← 输入：42 节预习目录（随营期推进逐节填充）
│   ├── __index__.md             42 节总目录 + 每节状态（⚪ / 🟡 / ✅）
│   ├── ai-fundamentals/         AI 基础（11 节）：LLM / Prompt / Context / RAG / Agent / Frameworks ...
│   ├── web3-fundamentals/       Web3 基础（10 节）：钱包 / 合约 / EVM / AA / DeFi / Oracle ...
│   ├── ai-web3-bridge/          交叉地带（15 节）：Agent Wallet / Machine Payment / Verifiable AI ...
│   └── frontier/                前沿探索（6 节）：Agentic Commerce / AI Wallet / Open Track ...
│
├── daily-log/                 ← 过程：每周一个文件夹，每天一个文件夹
│   ├── __index__.md             整套规范和模板
│   ├── week-1/                  Week 1: 建立共同语言
│   │   ├── __index__.md           当周索引（每日打卡进度一目了然）
│   │   ├── WEEK.md                当周完整目标和材料
│   │   ├── 2026-05-17/            一天一个文件夹
│   │   │   ├── __index__.md         当日概览 + 参考链接
│   │   │   ├── 2026-05-17.md        学习笔记本体
│   │   │   ├── TASK.md              任务、产出、交付证明
│   │   │   └── assets/              截图和图片
│   │   └── ...
│   ├── week-2/                  交叉方向深入
│   ├── week-3/                  Hackathon 启动
│   └── week-4/                  集中开发 + 提交
│
├── hackathon/                 ← 输出：最终项目
│   ├── contracts/               合约源码（提交时带上测试网 Tx Hash）
│   └── demo/                    演示材料：截图、视频、slides
│
├── idea/                      ← 实验：可复用 skill 原型 + 迭代参考
│   ├── skills/                  正式 skill（SKILL.md 格式）
│   │   ├── pre-study-note/      预习笔记整理
│   │   └── daily-log-sync/      每日日志同步
│   ├── reference/               经典案例 + 进化规范
│   └── workflows/               可固化的 workflow 模式
│
└── reference/                 ← 自己定的几条规矩，比如 commit 格式
    └── git-commit-reference.md
```

我自己用起来的逻辑就一句话：**`pre_study/` 是我带进营的弹药，`daily-log/` 是每天打仗的过程，`hackathon/` 是最后这场仗的成果。**

## 我带进营的几个判断

把预习目录梳过一遍之后，有些东西已经不再是"知识点"，而是会影响我后面怎么做项目的工作假设。先写在这里，等真正深入每一节、做完 Hackathon 之后再回来修订。

**关于 AI——**

模型输出永远是"候选答案"，不是事实。越靠近能改变世界的执行层（写文件、发交易、扣钱），越要把这种候选答案变成可被代码验证的对象。Prompt 是软约束，真正能拦住坏事的是代码、权限、校验、审计。

我现在最警惕的一种 Agent 设计是：模糊的目标 + 广泛的工具 + 长期记忆 + 直接动钱的权限。这四个凑齐了，几乎一定会出事。

**关于 Web3——**

私钥就是控制权本身，丢了不能找回，泄漏就是裸奔。钱包交互三层权限——只读（连接地址）< 签名消息 < 发交易——很多人以为自己在做第一层，其实点了第三层。

Session Key 在我看来是 Agent Wallet 的胜负手：**可限制 + 可过期 + 可撤销**——少一个都不够。

**关于交叉地带——**

Agent 不应该拥有"钱包"，它应该只拥有一组**可限制、可审计、可撤销**的能力。把私钥扔给 Agent 是当代版本的 root 权限滥用。

机器之间的支付，关键是预算先于执行、报价必须有有效期、付款后留下能验证交付的收据。这套东西链下做不干净，链上的 Escrow 状态机刚好补这个缺口。

可验证 AI 不必一上来就上 zkML，按风险分层就行。**Audit Trail 是最容易、也最先该落地的那层。**

## 我在考虑的 Hackathon 方向

Week 1-2 还在边学边筛，目前桌上的几个选项：

1. **Smart Account + Session Key 让 Agent 安全干活**——给 AI 一把"只能在某段时间、某个金额内、做某类事"的钥匙
2. **Agentic Commerce 闭环**——智能体从决策到链上执行到 DeFi 组合，再到出错时怎么回滚
3. **AI-native Wallet**——重新设计钱包确认 UX，让用户每一次签名都真正知道自己在批准什么
4. **链上数据分析 Agent**——把"看 Etherscan 看到累"这件事自动化

不管最后选哪个，硬性要求都一样：**必须有测试网 Tx Hash**，证明它真的在链上跑过，不是 PPT 项目。

## 一些关键链接

| 用途 | 链接 |
|------|------|
| 营期官网 | <https://aiweb3.school/> |
| 中文预习资料 | <https://aiweb3.school/zh/> |
| WCB 任务平台 | <https://web3career.build/zh/programs/AI-Web3-School?tab=apply> |
| Builder Profile | <https://web3career.build/profile> |
| Telegram 学员群 | <https://t.me/aiweb3school> |

## 合作生态（顺便记一笔）

- **LI.FI** — 跨链执行、流动性聚合、Intent/Solver 架构。如果做 Agentic Commerce，他们的 SDK 应该是绕不开的入口。
- **Waterdrip Capital** — 黑客松评审、资源对接、算力支持。值得在 Demo 阶段争取真实的反馈。

---

> 如果你顺着 git log 翻到这里——欢迎，这是我的实验现场，乱归乱，但每一个 commit 都是真的。

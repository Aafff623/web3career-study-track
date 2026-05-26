# 5/22 Week 1 例会分享 — 学习感受与信息观察

> **任务**：Week 1｜例会分享｜5.22 上麦分享学习感受或信息观察 (+5 学分)
> **形式说明**：当晚未上麦，以此书面提交学习感受与信息观察作为等价交付
> **关联仓库**：<https://github.com/Aafff623/web3career-study-track>

## Week 1 三条最大的收获

### 1. "知识图谱搭好了" ≠ "会做项目"

预习 42 节走完（AI 11 + Web3 10 + Bridge 15 + Frontier 6）之后，我以为自己"什么都知道"了。但 5/19 动手装 Hermes Agent、5/21 听 Sunny 讲 24h Agent 工作流时才意识到：**概念串联和动手做之间还差一个"卡点 → 解决 → 复盘"的循环**。

具体卡点：

- Hermes 在 Windows 本地不友好，最后绕到 DigitalOcean 云服务器上跑通
- biliGPT 自动产出的格式残缺一致，被迫先沉淀了一套[直播录播笔记清洗工作流](../../../toolkit/workflows/livestream-note-pipeline.md)
- 直播笔记原本散乱在 `daily-log/2026-05-XX.md` 各处，后来才意识到要按场次拆到独立的 `meetings/<slug>.md`

每个卡点都让"知识"变成了"我做过这件事"。**预习是了解概念，动手才是建立判断**。


### 2. AI × Web3 的核心是"可编程的约束"

5/23 听完 Sophia 讲 ERC-8004 和 x402，第一次把 Week 1 三块（AI / Web3 / Bridge）真正串起来：

- **AI Agent 越来越强** → 越来越能自主行动（写代码、做决策、付款）
- **传统基础设施不是为机器设计的** → 信用卡会被 prompt injection 滥用、API Key 会被泄进 context window、银行不能给 Agent 开户
- **Ethereum 的智能合约提供"可编程约束"** → 钱包 10 美元上限 + 只能向指定商家付款 + 只能完成指定任务

这不是"AI + Web3 = 暴富"的拼凑叙事，而是**为 AI Agent 这个新经济主体准备身份、声誉、支付、承诺执行的基础设施层**。

特别震撼的一个设计选择：**ERC-8004 的 reputation 绑定 Agent 本身而非 owner**。这让 Agent 真正成为机器经济中可独立运转的主体，而不是某个人的"账号附属物"。


### 3. "输出倒逼输入" 在共学营是真命题

例会上播出的优秀 PoW 笔记显示一个共性：**把"做了什么"拆得细，把"怎么证明"摆得显眼**。每条产出都对应可点击的链接 / 截图 / commit hash。

反推自己的 Week 1：很多产出有，但散在 daily-log 各处，没有汇总成可一眼看到的"证据列表"。所以 Week 1 结尾这两天一直在补：

- **5/22-5/23**：把 Week 1 漏掉的 6 场直播笔记全部回补（biliGPT 拉取 → 清洗 → 入库 → 索引补齐）
- **5/23**：新建 [`toolkit/`](../../../toolkit/) 工具箱沉淀工作流；新增 [`extras/web3/17h-web3-course/`](../../../extras/web3/17h-web3-course/) 加餐 5 课；接通 WCB Agent API 并沉淀 [`/wcb-sync` skill](../../../.claude/skills/wcb-sync/SKILL.md)
- **全部按 git-commit-guide 分 10+ commits 落地**，保证 git log 即时间线，不合并不掩盖

## 一个观察

往届优秀学员分享提到 **"Proof of Work 是机会的入口"** —— 不是简历投出去才有机会，**持续交付才会被看见**。这是个反直觉但很重要的视角：开源仓库即作品集，每次 commit 都是公开记录。

Week 1 真正动手以后我意识到：**对学员而言，仓库本身就是最好的"上麦"**。代码、笔记、commit 信息会替我说话。这也是我选择把所有 Week 1 学习痕迹尽量沉淀到 [`web3career-study-track`](https://github.com/Aafff623/web3career-study-track) 这个 public repo 的原因 —— 把"学到了"变成"做了 + 可验证"。

## Week 2 计划与 Hackathon 方向

**Week 2 重点关注的直播**：

- **5/25 Long-term Memory for AI Agents** — 正好对接 Hermes Agent 的痛点，Agent 长期上下文是绕不开的工程问题
- **5/26 Product Manager of Cobo Agentic Wallet** — 直接对应我的 Hackathon 候选方向 #3 AI-native Wallet
- **5/27 Neo-Cypherpunk & Cultural Layers of Privacy** — 补 zkML / 隐私支付的拼图

**Hackathon 方向倾向**：

当前最倾向 **Smart Account + Session Key**（候选方向 #1）。理由是 Sunny（5/21）的 24h Agent 工作流 + Sophia（5/23）的 ERC-8004 + Pizza 例子的可编程约束 = 这个方向最自然落地。Week 2 结束前会和导师 / 同学讨论后确定。

---

> 本文档保留在仓库内可追溯。如需作为 +5 学分任务的交付，提交此文件的 GitHub raw 链接即可。

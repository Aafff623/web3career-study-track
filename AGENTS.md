# AGENTS.md

> Codex 接入本项目时的方向与决策指引。项目级通用规范见 [`GUIDE.md`](./GUIDE.md)。

## 核心目标

1. **完成 4 周共学营全部打卡**——每天有记录，不断档
2. **产出可演示的 Hackathon 项目**——附测试网 Tx Hash
3. **建立可验证的 Builder Profile**——WCB 平台上有完整轨迹

## 当前阶段

- [x] 预习目录就位（42 节占位 README 已建，详见 [`pre_study/__index__.md`](./pre_study/__index__.md)）
- [ ] Week 1：建立共同语言（05/17 - 05/23）·  进行中 🟢
- [ ] Week 2：交叉方向深入（05/24 - 05/30）
- [ ] Week 3：Hackathon 启动（05/31 - 06/06）
- [ ] Week 4：集中开发提交（06/07 - 06/14）

## 决策记录

| 日期 | 决策 | 原因 |
|------|------|------|
| 05-17 | 仓库结构确定：daily-log + pre_study + hackathon | 对应输入→过程→输出三阶段 |
| | Hackathon 方向待定 | Week 1-2 先学习再选方向 |
| 05-22 | 新建 `extras/` 加餐模块 | 给课程外 B 站/博客/Twitter 碎片一个归属地 |
| 05-23 | 新建 `toolkit/` 工具箱 + 直播录播笔记规范 | biliGPT 输出沉淀路径标准化，与 extras（学习内容）互补 |

## 优先级原则

1. **每日打卡 > 笔记完美度**——先交再改，不要因为整理笔记而错过打卡
2. **理解 > 记录**——笔记是帮助理解的工具，不是目的
3. **可演示 > 功能完整**——Hackathon 项目做出闭环 Demo 比功能多更重要
4. **链上证明 > 本地运行**——部署到测试网是硬性要求

## Hackathon 候选方向

> Week 2 结束前确定，选一个深入

1. Smart Account + Session Key（AI Agent 安全执行链上操作）
2. Agentic Commerce 闭环（智能体决策→链上执行→验收）
3. AI-native Wallet（重新设计钱包确认 UX）
4. On-chain Data Analysis Agent（链上数据分析智能体）

## 风险与注意

- 前两周不能划水，否则 Week 3-4 接不住 Hackathon
- 项目提交必须有测试网 Tx Hash，不能只有本地代码
- 注意保护私钥/助记词，不要提交到仓库

## Codex 行为约定

1. **不要假设** —— 不确定时先问，不要凭空补全缺失信息
2. **最小改动** —— 只改用户要求的部分，不顺手重构无关代码
3. **先理解再动手** —— 阅读相关文件和上下文后再给出方案
4. **保持风格一致** —— 匹配项目现有的 Markdown 格式和命名规范
5. **不要自动 commit & push** —— 完成任务后等用户 review 并明确授权

---

## Learning Agent Prompt（辅助）

> 来源：https://aiweb3.school/learning-agent.zh.txt

以下是官方 Learning Agent 启动提示词，作为上述约束的补充参考。

### 角色

你是 AI × Web3 School 学员的个人 Learning Agent。你的目标不是替学员完成学习，而是帮助学员理解课程、规划每日任务、维护个人学习仓库、生成打卡草稿、提醒同步到 WCB / 打卡平台，并把学习过程中的问题沉淀为可开源、可索引、可复盘的材料。

### 固定入口

- Handbook：https://aiweb3.school/zh/handbook/
- WCB 课程页面：https://web3career.build/zh/programs/AI-Web3-School
- WCB Learning 页面：https://web3career.build/zh/programs/AI-Web3-School#tab=learning
- WCB Agent API 文档：https://web3career.build/llms.txt
- GitHub 官网：https://github.com/
- GitHub CLI：https://cli.github.com/

如果某个页面打不开，不要猜测内容；请告诉学员打开对应链接确认。

### 每日学习与打卡

每天早上可以提醒一次，晚上可以提醒一次。不同学员可根据自己的节奏选择只开早上、只开晚上或早晚两次。

每日流程：

1. 读取 WCB Learning 页面，确认今日课程、任务、会议和打卡入口。
2. 读取 Handbook 相关章节，生成今日最小路径、推荐路径、挑战路径。
3. 帮学员写 `daily/YYYY-MM-DD.md`。
4. 生成打卡草稿。
5. 返回 WCB / 打卡平台链接，让学员手动打开并提交。
6. 学员提交后，把打卡链接或提交记录写回 daily note。

不要承诺可以从 Agent 里自动一键同步到原生平台。更稳妥的默认行为是：生成打卡内容 + 返回打卡链接 + 学员手动确认提交。

### Handbook feedback

学员在学习中的问题、卡点、错别字、概念不清楚、资料过期、结构建议，应整理到个人 repo 的 `handbook-feedback/` 目录下。

每条 feedback 尽量包含：Handbook 页面链接、问题描述、建议改法和来源。

### WCB Agent API 与 secrets

如果需要连接 WCB Agent API：

- Base URL 使用线上：https://web3career.build
- API 文档：https://web3career.build/llms.txt
- Secret API Key 只放在本地环境变量或 Hermes secrets 中，例如 `WCB_AGENT_SECRET_API_KEY`。
- 不要把 secret 写进 prompt、README、聊天记录或公开 repo。
- 所有写入型操作，例如提交任务、更新资料、创建记录，都必须先展示将要写入的内容并取得学员确认。

### 设计原则

- 轻量优先：先让学员今天能行动，而不是一次性规划所有未来。
- 人工确认：涉及账号、repo、写文件、打卡、WCB 提交、secret 配置的步骤必须确认。
- 开源沉淀：repo 是 proof-of-work workspace，不只是笔记。
- 隐私安全：public repo 不放敏感信息。
- Handbook 反馈闭环：学员问题要能回流到 Handbook feedback。
- 平台边界清楚：Agent 辅助生成和提醒，正式提交以 WCB / 打卡平台为准。

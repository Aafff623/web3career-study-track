# AI Web3 School BootCamp 学习记录

> 4 周线上共学营 + 黑客松 | 主题：AI × Web3 交叉方向  
> 状态：进行中 | 开营：2026-05-17

## 项目定位

当 AI Agent 能调用工具、读写数据、触发支付时，**谁授权、谁付款、责任边界在哪里**——这正是 Web3 基础设施（钱包、签名、智能合约、账户抽象）要解决的问题。

本仓库记录从预习到 Hackathon 全程的学习笔记、每日产出与项目交付。

---

## 学习节奏

| 阶段 | 时间 | 内容 | 产出 |
|------|------|------|------|
| Week 1 | 05/17 - 05/23 | 建立 AI 与 Web3 的共同语言 | 基础概念笔记、Co-Learning 打卡 |
| Week 2 | 05/24 - 05/30 | AI × Web3 交叉方向深入 | Bridge 模块笔记、分享会记录 |
| Week 3 | 05/31 - 06/06 | 实践深化 + Hackathon 启动 | 项目方向确定、初步实现 |
| Week 4 | 06/07 - 06/14 | 集中开发、提交与 Demo 展示 | 项目代码 + 测试网 Tx Hash |

每天有：课程/分享会 → Co-Learning 讨论 → 任务打卡 → 产出提交

---

## 仓库结构

```
web3career-study-track/
│
├── README.md                          ← 本文件（总览 + 核心提炼）
│
├── daily-log/                         ← 【每日记录】按周→日两层组织
│   ├── __index__.md                    规范说明 + 模板
│   ├── week-1/                        Week 1: 05/17 - 05/23 建立共同语言
│   │   ├── __index__.md                当周概览 + 每日索引表
│   │   ├── WEEK.md                     当周完整目标、任务、推荐材料
│   │   ├── 2026-05-17/                每天一个文件夹
│   │   │   ├── __index__.md            当日索引：概览、参考链接
│   │   │   ├── 2026-05-17.md           学习笔记
│   │   │   ├── TASK.md                 任务与产出、交付证明
│   │   │   └── assets/                 截图、图片
│   │   ├── ...
│   │   └── 2026-05-23/
│   ├── week-2/                        Week 2: 05/24 - 05/30 交叉方向深入
│   ├── week-3/                        Week 3: 05/31 - 06/06 Hackathon 启动
│   └── week-4/                        Week 4: 06/07 - 06/14 集中开发 + 提交
│
├── pre_study/                         ← 【预习阶段】开营前完成的 42 节知识笔记
│   │
│   ├── ai-fundamentals/              ← 模块一：AI 基础（11 节）
│   │   ├── LLM/                       Token、Embedding、幻觉、模型在系统中的位置
│   │   ├── Prompt/                    指令设计、Few-shot、结构化输出、Prompt Injection
│   │   ├── Context/                   上下文窗口、Context Engineering、Memory
│   │   ├── RAG/                       切分、向量库、检索、Rerank、Citation
│   │   ├── Agent/                     工具调用、规划、状态、反思、多智能体
│   │   ├── Frameworks/                LangChain、LangGraph、OpenAI Agents SDK、DSPy
│   │   ├── Vibe-Coding/              Claude Code、Codex CLI、人机协作工作流
│   │   ├── MCP/                       模型上下文协议：Server/Client/Tool Schema/Permission
│   │   ├── Evaluation/                评估框架、Golden Set、LLM-as-Judge、回归测试
│   │   ├── Fine-tuning/              SFT、LoRA、PEFT、数据集、过拟合
│   │   └── Inference/                 API 模型、本地模型、量化、推理服务部署
│   │
│   ├── web3-fundamentals/            ← 模块二：Web3 基础（10 节）
│   │   ├── Cryptography/              Hash、公私钥、签名、Merkle Tree
│   │   ├── Wallet/                    EOA、助记词、交易三层权限、Gas
│   │   ├── Smart-Contract/            Solidity、EVM、ABI、Event、升级
│   │   ├── Dev-Stack/                 Remix、Hardhat、Foundry、OpenZeppelin、viem/wagmi
│   │   ├── Network/                   区块、共识、PoS、测试网、L2、Rollup
│   │   ├── Account-Abstraction/       ERC-4337、Smart Account、Bundler、Paymaster、Session Key
│   │   ├── DeFi/                      Token、AMM、借贷、稳定币、流动性
│   │   ├── Oracle/                    Price Feed、Data Feed、Oracle 风险
│   │   ├── Indexing/                  Event 索引、Subgraph、RPC、数据管道
│   │   └── Security/                  重入、权限控制、审计、模拟、监控
│   │
│   ├── ai-web3-bridge/              ← 模块三：AI × Web3 交叉（15 节）
│   │   ├── Chain-aware-Context/       链上数据如何进入 AI 上下文（带 citation + 时间戳）
│   │   ├── Web3-Tool-Use/            RPC/读/写工具分离、权限、日志
│   │   ├── Agent-Workflow/           任务图、状态机、Human-in-the-loop、Trace
│   │   ├── Agent-Wallet/            AA 钱包、Session Key、Policy、Guard、模拟、撤销
│   │   ├── Machine-Payment/          预算、报价、Payment Intent、x402、订阅
│   │   ├── Settlement-and-Escrow/    Escrow 状态机、收据、交付证明、争议仲裁
│   │   ├── Agent-Identity/           Agent Profile、能力声明、DID/VC、注册表
│   │   ├── Agent-Trust-and-Reputation/ 声誉、Attestation、Stake、Slashing
│   │   ├── AI-Oracle/                AI 输出上链、Proof of Inference、争议机制
│   │   ├── Verifiable-AI/            TEE、ZK、zkML、审计追踪、按风险分层
│   │   ├── AI-Security/              Prompt Injection 防护、工具滥用、权限隔离
│   │   ├── AI-Privacy/               数据边界、本地 AI、最小披露
│   │   ├── AI-Sovereignty/           用户控制、数据可迁移、d/acc、CROPS
│   │   ├── Governance-AI/            提案摘要、来源可追溯、人保留决策权
│   │   └── Decentralized-AI/         模型市场、算力市场、推理网络、结算
│   │
│   └── frontier/                     ← 模块四：前沿探索（6 节）
│       ├── Agentic-Commerce/          购买意图结构化、预算分层、Escrow 闭环
│       ├── Dev-Tooling/               文档→Agent、合约阅读、交易解释、测试生成
│       ├── Wallet-and-Permission/     AI 钱包 UX、Permission Policy、Session Key 流程
│       ├── AI-Security/               威胁模型、工具权限隔离、行为审计
│       ├── Governance/                提案摘要器、会议→行动、预算检查、多元视角
│       └── Open-Track/                AI-native Wallet、链上数据分析、跨赛道组合
│
└── hackathon/                        ← 【产出阶段】Hackathon 项目代码与演示
    ├── contracts/                     智能合约源码（提交时附测试网 Tx Hash）
    └── demo/                          Demo 演示材料（截图、视频、slides）
```

**逻辑：** `pre_study/` 是输入（知识储备）→ `daily-log/` 是过程（每日打卡与产出）→ `hackathon/` 是输出（最终交付）

---

## 核心认知提炼

### AI 基础

- 模型输出是候选结果，不是事实——越靠近执行层，越要把输出变成可验证对象
- Prompt 是软约束，真正的边界由代码、权限、校验和审计承担
- Agent 最危险的设计：同时拥有模糊目标 + 广泛工具 + 长期记忆 + 大额资产权限
- MCP 解决"怎么接"，不解决"谁有权限接"

### Web3 基础

- 私钥是控制权本身，丢了无法找回，泄漏意味着失去一切
- 钱包交互三层权限：连接（读地址）< 签名消息 < 发送交易（改变链上状态）
- Session Key 是 Agent Wallet 的关键：可限制 + 可过期 + 可撤销
- Web3 安全 = 权限最小化 + 执行前模拟 + 上线后监控

### AI × Web3 Bridge

- Agent Wallet 不给主私钥，用 Session Key 给受限能力，自动化必须绑定撤销能力
- 机器支付：预算先于执行，报价必须有有效期，付款后留收据
- AI Oracle 结果要结构化，争议要提前设计，不能让模型直接替合约做判断
- 可验证 AI 按风险分层；Audit Trail 是最容易落地的起点
- 不可信输入无法直接变成不受限执行

### 前沿探索

- Agentic Commerce = 购买意图结构化 + 预算分层 + 任务完成证明 + Escrow 状态机
- Agent 不应该拥有"钱包"，只应该拥有可限制、可审计、可撤销的能力
- AI 安全靠结构隔离，不靠"更聪明的 prompt"
- 开放赛道评估三问：AI 不可替代什么？Web3 不可替代什么？两周内能做出可演示闭环吗？

---

## Hackathon 方向建议

1. **Smart Account + Session Key**：让 AI Agent 安全地执行链上操作
2. **Agentic Commerce 闭环**：智能体决策 → 链上执行 → DeFi 组合 → 故障恢复
3. **AI-native Wallet**：重新设计钱包 UX，让确认有意义
4. **On-chain Data Analysis Agent**：链上数据分析智能体

项目提交必须附**测试网 Tx Hash**，证明代码真正在链上跑过。

---

## 关键链接

| 资源 | 链接 |
|------|------|
| 官网 | https://aiweb3.school/ |
| 预习资料（中文） | https://aiweb3.school/zh/ |
| WCB 平台 | https://web3career.build/zh/programs/AI-Web3-School?tab=apply |
| Builder Profile | https://web3career.build/profile |
| Telegram 群 | https://t.me/aiweb3school |

---

## 合作生态

- **LI.FI**：跨链执行、流动性聚合、Intent/Solver 架构、Agentic Commerce
- **Waterdrip Capital**：黑客松评审、资源对接、算力支持、项目孵化

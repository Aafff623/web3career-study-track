# pre_study ｜ 前置学习参考笔记总目录大纲

> 4 大模块 · 42 节笔记 · 开营前的弹药库

## 介绍

对应营期正式开始前的自学储备。每个主题对应一个文件夹，里面的 `README.md` 就是该主题的完整笔记。

笔记会随着我把官网章节内容陆续粘给 `Kiro `整理,模版初始化 结构排版,  然后迭代自己的人工批注和感悟想法,   而非单纯的 AI 堆积屎山 —— 因此本目录是**渐进式建设**的，不是一次性写完。

## RoadMap

> 这是我读完 [Handbook 引言](https://aiweb3.school/zh/) 后整理的地图，不是逐字复述。引用来源放在末尾。

AI × Web3 不是把两个 buzzword 拼在一起。一个真实系统会同时撞上这些问题：

- 模型怎么理解任务、组织上下文、调用工具
- Agent 怎么从"回答问题"进到"执行流程"
- 钱包和账户怎么表达权限、额度、时间和撤销条件
- 链上交易怎么被模拟、确认、记录和审计
- 支付、身份、声誉、治理怎么接入自动化系统
- 隐私、安全和可验证性怎么在产品里落地

**任何一边单独看都会出现盲区**

​	只从 AI 侧看会低估资产和权限风险；只从 Web3 侧看又容易忽略模型、上下文和工具编排的复杂度。

因此需要先**建立一套共同语言**：概念, 边界, 最小实践

### 四层地图

| 分层 | 在解决什么问题 |
|----|--------------|
| **AI 基础** | 模型和应用系统怎么搭——LLM / Prompt / Context / RAG / Agent / Frameworks / MCP / Evaluation |
| **Web3 基础** | 链上系统怎么跑——Network / Cryptography / Wallet / Smart Contract / AA / DeFi / Oracle / Indexing / Security |
| **AI × Web3 Bridge** | 真正的交叉问题——Agent 读链上状态、调工具、拿权限、做支付、留可验证记录 |
| **前沿探索** | 把上面的节点组合成可演示、可扩展的原型 |

### 不同起点的推荐路径

| 我的处境 | 怎么进 |
|---------|-------|
| 缺 AI 基础 | LLM → Prompt → Context → RAG → Agent |
| 缺 Web3 基础 | Network → Cryptography → Wallet → Smart Contract → AA |
| 两边都熟 | 直接进 Bridge：链上状态进上下文、工具调用、权限管理、支付结算 |
| 在准备 Hackathon | 从**前沿探索**开始，先组合出一个小原型，别停在概念 |

**问题反查路径**（如果已经在做具体产品）：

- 做交易解释器 → `LLM` · `Context` · `Chain-aware Context`
- 做链上 Agent → `Agent` · `Web3 Tool Use` · `Agent Workflow`
- 做钱包 / 自动支付 → `Wallet` · `Account Abstraction` · `Agent Wallet`
- 做安全 / 风控 → `Prompt` · `RAG` · `AI Security`

### 这事儿背后的更大目标

学习和实践连起来：

> **问题定义 → 共学训练 → 项目实践 → 对外展示 → 人才与机会沉淀**

后续 builders 仍能从这里进入、继续修正补充共建长期的资产。

## 命名约定

```
pre_study/<module>/<Topic>/README.md
```

- 每个主题一个文件夹，文件夹名用英文（避免链接编码问题）
- 笔记本体统一叫 `README.md`，GitHub 网页点进文件夹会自动渲染
- 引用方式：`[LLM 笔记](../pre_study/ai-fundamentals/LLM/README.md)`

## 完成进度

> 状态图例：⚪ 未开始 · 🟡 整理中 · ✅ 已完成

### 模块一 · AI 基础（11 节）

| 状态 | 主题 | 笔记 | 一句话定位 |
|------|------|------|-----------|
| ⚪ | LLM | [📝](./ai-fundamentals/LLM/README.md) | Token、Embedding、幻觉、模型在系统中的位置 |
| ⚪ | Prompt | [📝](./ai-fundamentals/Prompt/README.md) | 指令设计、Few-shot、结构化输出、Prompt Injection |
| ⚪ | Context | [📝](./ai-fundamentals/Context/README.md) | 上下文窗口、Context Engineering、Memory |
| ⚪ | RAG | [📝](./ai-fundamentals/RAG/README.md) | 切分、向量库、检索、Rerank、Citation |
| ⚪ | Agent | [📝](./ai-fundamentals/Agent/README.md) | 工具调用、规划、状态、反思、多智能体 |
| ⚪ | Frameworks | [📝](./ai-fundamentals/Frameworks/README.md) | LangChain、LangGraph、OpenAI Agents SDK、DSPy |
| ⚪ | Vibe-Coding | [📝](./ai-fundamentals/Vibe-Coding/README.md) | Claude Code、Codex CLI、人机协作工作流 |
| ⚪ | MCP | [📝](./ai-fundamentals/MCP/README.md) | Server / Client / Tool Schema / Permission |
| ⚪ | Evaluation | [📝](./ai-fundamentals/Evaluation/README.md) | 评估框架、Golden Set、LLM-as-Judge、回归测试 |
| ⚪ | Fine-tuning | [📝](./ai-fundamentals/Fine-tuning/README.md) | SFT、LoRA、PEFT、数据集、过拟合 |
| ⚪ | Inference | [📝](./ai-fundamentals/Inference/README.md) | API 模型、本地模型、量化、推理服务部署 |

### 模块二 · Web3 基础（10 节）

| 状态 | 主题 | 笔记 | 一句话定位 |
|------|------|------|-----------|
| ⚪ | Cryptography | [📝](./web3-fundamentals/Cryptography/README.md) | Hash、公私钥、签名、Merkle Tree |
| ⚪ | Wallet | [📝](./web3-fundamentals/Wallet/README.md) | EOA、助记词、交易三层权限、Gas |
| ⚪ | Smart-Contract | [📝](./web3-fundamentals/Smart-Contract/README.md) | Solidity、EVM、ABI、Event、升级 |
| ⚪ | Dev-Stack | [📝](./web3-fundamentals/Dev-Stack/README.md) | Remix、Hardhat、Foundry、OpenZeppelin、viem / wagmi |
| ⚪ | Network | [📝](./web3-fundamentals/Network/README.md) | 区块、共识、PoS、测试网、L2、Rollup |
| ⚪ | Account-Abstraction | [📝](./web3-fundamentals/Account-Abstraction/README.md) | ERC-4337、Smart Account、Bundler、Paymaster、Session Key |
| ⚪ | DeFi | [📝](./web3-fundamentals/DeFi/README.md) | Token、AMM、借贷、稳定币、流动性 |
| ⚪ | Oracle | [📝](./web3-fundamentals/Oracle/README.md) | Price Feed、Data Feed、Oracle 风险 |
| ⚪ | Indexing | [📝](./web3-fundamentals/Indexing/README.md) | Event 索引、Subgraph、RPC、数据管道 |
| ⚪ | Security | [📝](./web3-fundamentals/Security/README.md) | 重入、权限控制、审计、模拟、监控 |

### 模块三 · AI × Web3 交叉（15 节）

| 状态 | 主题 | 笔记 | 一句话定位 |
|------|------|------|-----------|
| ⚪ | Chain-aware-Context | [📝](./ai-web3-bridge/Chain-aware-Context/README.md) | 链上数据进入 AI 上下文（带 citation + 时间戳） |
| ⚪ | Web3-Tool-Use | [📝](./ai-web3-bridge/Web3-Tool-Use/README.md) | RPC / 读 / 写工具分离、权限、日志 |
| ⚪ | Agent-Workflow | [📝](./ai-web3-bridge/Agent-Workflow/README.md) | 任务图、状态机、Human-in-the-loop、Trace |
| ⚪ | Agent-Wallet | [📝](./ai-web3-bridge/Agent-Wallet/README.md) | AA 钱包、Session Key、Policy、Guard、模拟、撤销 |
| ⚪ | Machine-Payment | [📝](./ai-web3-bridge/Machine-Payment/README.md) | 预算、报价、Payment Intent、x402、订阅 |
| ⚪ | Settlement-and-Escrow | [📝](./ai-web3-bridge/Settlement-and-Escrow/README.md) | Escrow 状态机、收据、交付证明、争议仲裁 |
| ⚪ | Agent-Identity | [📝](./ai-web3-bridge/Agent-Identity/README.md) | Agent Profile、能力声明、DID / VC、注册表 |
| ⚪ | Agent-Trust-and-Reputation | [📝](./ai-web3-bridge/Agent-Trust-and-Reputation/README.md) | 声誉、Attestation、Stake、Slashing |
| ⚪ | AI-Oracle | [📝](./ai-web3-bridge/AI-Oracle/README.md) | AI 输出上链、Proof of Inference、争议机制 |
| ⚪ | Verifiable-AI | [📝](./ai-web3-bridge/Verifiable-AI/README.md) | TEE、ZK、zkML、审计追踪、按风险分层 |
| ⚪ | AI-Security | [📝](./ai-web3-bridge/AI-Security/README.md) | Prompt Injection 防护、工具滥用、权限隔离 |
| ⚪ | AI-Privacy | [📝](./ai-web3-bridge/AI-Privacy/README.md) | 数据边界、本地 AI、最小披露 |
| ⚪ | AI-Sovereignty | [📝](./ai-web3-bridge/AI-Sovereignty/README.md) | 用户控制、数据可迁移、d/acc、CROPS |
| ⚪ | Governance-AI | [📝](./ai-web3-bridge/Governance-AI/README.md) | 提案摘要、来源可追溯、人保留决策权 |
| ⚪ | Decentralized-AI | [📝](./ai-web3-bridge/Decentralized-AI/README.md) | 模型市场、算力市场、推理网络、结算 |

### 模块四 · 前沿探索（6 节）

| 状态 | 主题 | 笔记 | 一句话定位 |
|------|------|------|-----------|
| ⚪ | Agentic-Commerce | [📝](./frontier/Agentic-Commerce/README.md) | 购买意图结构化、预算分层、Escrow 闭环 |
| ⚪ | Dev-Tooling | [📝](./frontier/Dev-Tooling/README.md) | 文档→Agent、合约阅读、交易解释、测试生成 |
| ⚪ | Wallet-and-Permission | [📝](./frontier/Wallet-and-Permission/README.md) | AI 钱包 UX、Permission Policy、Session Key 流程 |
| ⚪ | AI-Security | [📝](./frontier/AI-Security/README.md) | 威胁模型、工具权限隔离、行为审计 |
| ⚪ | Governance | [📝](./frontier/Governance/README.md) | 提案摘要器、会议→行动、预算检查、多元视角 |
| ⚪ | Open-Track | [📝](./frontier/Open-Track/README.md) | AI-native Wallet、链上数据分析、跨赛道组合 |

## 总进度

| 模块 | 已完成 / 总数 |
|------|--------------|
| AI 基础 | 0 / 11 |
| Web3 基础 | 0 / 10 |
| AI × Web3 交叉 | 0 / 15 |
| 前沿探索 | 0 / 6 |
| **合计** | **0 / 42** |

> 每完成一节 Agent 就回到这里更新 并且 维护 对应行的状态和总进度数字, 在通过人工的review微调, 进行 commit & push

## 关于鞭策 Agent 的维护迭代

- **整理一节**：把官网章节参考的知识内容粘给 Kiro，让它以 原文 + 批注的形式进行整理
- **日常引用**：在 `daily-log/.../YYYY-MM-DD.md` 里直接链接到对应主题的 README.md，不重复展开内容。daily-log 重点撰写该天的心得体会经验
- **批量回顾**：每次改动文件目录 / 人工要求维护的时候扫一眼本表，看看哪些主题还没动，对照 `daily-log/week-N/WEEK.md` 的实际推进度调整优先级。


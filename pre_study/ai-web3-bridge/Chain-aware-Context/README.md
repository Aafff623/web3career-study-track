# Chain-aware Context

> 模块：AI × Web3 交叉 · 状态：✅ 已完成

## 链感知上下文（Chain-aware Context）

Chain-aware Context 指的是让 AI 在回答或行动前，能看见正确的链、地址、合约、交易、事件、余额、授权和数据来源，而不是只靠用户一句话猜测链上状态。

### 为什么要学这个

普通 AI 应用的上下文通常来自文档、聊天历史、数据库和网页。AI x Web3 多了一层：链上状态会持续变化，而且很多状态和资产、权限、交易执行直接相关。

如果 Agent 不知道当前 chain id、合约地址、ABI、用户授权、交易历史和数据更新时间，它就可能给出错误建议，甚至生成危险交易。

链感知上下文的核心，是把链上事实变成模型可读、可引用、可验证的上下文。

> *知识节点：链上事实 ≠ 语言记忆* 模型训练数据里没有"你钱包里现在有多少钱"。链上状态是动态的、具体的、带时间戳的，必须通过工具实时读取，不能靠模型"猜"。这是 AI×Web3 和普通 AI 应用的根本区别——上下文来源从静态文档变成了链上实时状态。


### 第一性原理

模型不能凭语言记忆判断链上事实，链上事实必须从工具和索引层读取。

模型知道"Uniswap 是 DEX"没有用，真正执行时需要知道具体网络、具体合约、具体池子、当前价格、用户余额、allowance、滑点和交易模拟结果。

链上状态有时间性：同一个地址的余额、授权和仓位会随区块变化。
上下文要带来源：合约地址、区块号、交易哈希、explorer 链接都应该能追溯。
上下文要区分事实和解释：工具返回事实，模型负责解释，不要把模型猜测当事实。

> *知识节点：三要素* 链感知上下文的三个硬性要求：**时间性**（同一个地址在不同区块的状态不同）、**可追溯**（每条数据必须带来源）、**事实与解释分离**（工具返回 raw data，模型只做 interpretation）。违反任何一条都会导致 Agent 基于错误前提做决策。


### 知识节点

#### On-chain Data

难度：初级。 On-chain Data 是链上可直接验证的数据，例如余额、交易、日志、合约状态和区块信息。

常见来源包括 RPC、区块浏览器、索引器和协议 API。对 Agent 来说，读取 on-chain data 时至少要带上：chain id、block number、contract address、method、返回值、读取时间。

如果缺少这些字段，模型很容易把不同链、不同时间和不同合约的数据混在一起。

> *知识节点：元数据不可省* 读链上数据时，chain id + block number + timestamp 是"这条数据是什么时候、从哪条链上拿到的"的证明。缺少这些，模型拿到的只是一堆数字，无法判断时效性和正确性。


#### Contract Docs

难度：初级。 Contract Docs 帮助模型理解合约的设计意图、参数含义、权限边界和使用方式。

ABI 只能告诉你函数签名，不能解释业务语义。比如 execute(bytes calldata data) 可能是普通执行，也可能是高权限入口。文档、NatSpec、README、审计报告和部署说明可以补足语义。

但文档也可能过期。Agent 读取文档后，仍要用链上数据验证：合约地址、版本、owner、proxy implementation、事件和最近交易是否匹配。

> *知识节点：ABI ≠ 语义* ABI 只是函数签名的编码规范，不包含业务意图。同一个 `execute` 函数在不同合约里权限完全不同。Agent 必须结合 NatSpec、文档和链上验证来理解合约"想做什么"，不能只看 ABI 猜。


#### ABI / Event

难度：中级。 ABI 和 Event 是 Agent 理解合约可调用能力和历史行为的核心结构。

ABI 让工具知道如何编码函数调用、解码返回值和解析事件。Event 则是合约向外部系统留下的业务日志，例如 Transfer、Swap、Deposit、VoteCast。

Agent 使用 ABI 时要小心：能调用不等于应该调用。写交易前还需要权限、余额、allowance、slippage、simulation 和 policy 检查。

相关 topic

- 智能合约（Smart Contract）：理解 ABI 和 event 在合约交互中的位置。
- 索引（Indexing）：继续看 event 如何进入索引层。

> *知识节点：能调用 ≠ 应该调用* ABI 告诉你"这个函数可以被调用"，但不告诉你"应不应该调用"。Agent 拿到 ABI 后直接生成 calldata 是危险的——还需要检查权限、余额、allowance、滑点和 policy。这是 Web3 Tool Use 的核心安全边界。


#### Transaction History

难度：中级。 Transaction History 帮助 Agent 理解用户或合约过去做过什么。

交易历史可以用于判断：用户是否已经授权，某个策略是否执行过，某个地址是否和高风险合约交互过，某个合约最近是否升级过。

但交易历史不能只看自然语言总结。至少要保留 transaction hash、block number、from、to、method、value、token transfers 和 logs。模型可以总结，但证据必须能回到链上。

> *知识节点：总结可丢，证据不能丢* Agent 可以用自然语言总结交易历史，但底层必须保留完整字段（tx hash, block, from/to, method, value, logs）。总结是给人看的，证据是给验证用的——出问题时需要能回到链上核验。


#### Explorer Context

难度：初级。 Explorer Context 是区块浏览器提供的可视化链上证据。

区块浏览器适合给用户和 Agent 提供可检查入口：交易是否成功、合约是否验证、源码是否公开、事件是否发出、token transfer 是否发生。

在 AI 产品里，给出 explorer link 比只给一句"交易成功"更可靠。用户可以自己打开链接核验，开发者也能排查错误。

> *知识节点：Link > 文字声明* "交易成功"只是一句话，explorer link 是可验证的证据。AI×Web3 产品应该默认给 explorer link，让用户和系统都能独立验证。这是建立信任的基础。


#### Indexing Context

难度：中级。 Indexing Context 是把链上事件整理成面向产品查询的数据。

Agent 需要的问题通常不是"某个区块里有什么"，而是"用户最近 30 天有哪些 DeFi 操作""这个池子的 TVL 变化如何""这个 Agent 做过哪些支付"。这类查询需要索引层。

索引上下文必须带时间戳和同步状态。一个落后 500 个区块的索引结果，不应该被 Agent 当成当前事实。

> *知识节点：索引有延迟* 索引器不是实时的，落后几百个区块很正常。Agent 使用索引数据时必须检查同步状态，否则会基于过期数据做决策——比如用旧价格估算 swap 结果。


#### Citation

难度：初级。 Citation 是让模型回答能回到具体链上证据或文档来源。

链上场景里，引用可以是交易哈希、区块号、合约地址、event log、explorer 链接、文档 URL、审计报告章节。Citation 的价值是让用户和系统知道：这句话基于什么事实。

没有 citation 的链上解释，只能算观点；带 citation 的解释，才有机会被验证和追责。

> *知识节点：Citation 是信任链* 在链上场景，citation 不是"学术引用"，而是"这条结论基于哪个区块的哪条数据"。没有 citation 的 Agent 输出 = 没有证据的证词，用户和系统都无法验证。这是 Agent 可审计性的基础。


### 在 AI x Web3 中的位置

Chain-aware Context 是所有链上 Agent 的输入层。没有这层，Web3 Tool Use、Agent Workflow、Agent Wallet 都会建立在不可靠上下文上。

一个好的链感知上下文包应该像这样：

- 用户目标；
- 当前 chain id 和网络名称；
- 用户地址和余额；
- 相关合约地址、ABI、文档和风险提示；
- 最近交易和授权；
- 索引数据更新时间；
- 每条关键结论的 citation。

> *知识节点：上下文包清单* 这 7 项是链感知上下文的最小完整包。缺任何一项，Agent 都可能在不完整信息下做决策。实际实现时可以按需裁剪，但裁剪的理由必须明确——不是"忘了加"，而是"这个场景不需要"。


### 最小实践

给一笔交易做上下文包：

1. 找一笔公开交易哈希。
2. 收集 chain id、block number、from、to、method、value、token transfers、logs。
3. 找到合约 ABI 或 verified source。
4. 写一段模型可读的上下文，但每个关键结论都附上交易哈希或 explorer 链接。
5. 标出哪些内容是链上事实，哪些是你的解释。


### 扩展阅读

- Ethereum JSON-RPC API：理解链上数据如何通过 RPC 被读取。
- Ethereum Events and Logs：理解事件和日志如何成为链上上下文来源。
- Etherscan API Docs：了解区块浏览器数据接口如何辅助查询交易、合约和地址。
- The Graph Subgraphs：学习如何把事件整理成可查询上下文。
- OpenAI Tools Guide：理解模型如何通过工具读取外部事实，而不是依赖记忆。

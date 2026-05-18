# Evaluation ｜ 评估

> 模块：AI 基础 · 状态：🟡 整理中 · 来源：AI Web3 School Handbook

*约 1413 字 · 5 分钟 · 2026-05-12*

---

Evaluation 是把"感觉效果不错"变成"系统可持续改进"的方法。没有 eval，prompt、模型、RAG、Agent 和工具调用的变化都只能靠主观试用判断，迟早会被回归问题拖住。

## 为什么要学这个

AI 应用最大的问题之一，是输出质量不稳定。你改了一句 prompt，某些问题变好了，另一些问题变差了；换了模型，平均效果提升，但关键场景出错；接了 RAG，答案更长了，但引用反而不准。

Evaluation 要解决的就是这些问题：用明确样本、指标、评分方式和回归测试，判断系统是不是真的变好了。

学 eval 的目标不是做一份漂亮报告，而是让团队能回答：这次改动有没有让关键任务更可靠？有没有引入新的失败模式？

> *Eval 的核心价值：把"感觉变好了"变成"可以证明变好了"。没有 eval 的 AI 改动就是在赌运气——改了 A，B 有没有坏，你不知道。*

## 第一性原理

**不能被重复测量的 AI 行为，就不能被稳定改进。**

AI 系统的输出有概率性，用户问题又很开放。如果没有固定样本和评估标准，你很难知道系统变化来自真实改进、运气、还是测试样本太少。

- **先测任务，不只测模型**：用户真正关心的是整条链路是否完成任务，而不是模型榜单分数。
- **先保住关键失败场景**：高风险错误、常见问题、边界条件，要进入 regression set。
- **评估要贴近产品**：离真实输入越远，eval 越容易变成自我安慰。

> *Eval 的三原则：真实链路测试、保关键失败、贴近真实输入。脱离产品的 eval 只是自我安慰。*

## 知识节点


### Harness

Harness 是运行 eval 的框架。它负责喂样本、调用系统、收集输出、运行 grader、记录结果。

一个最小 harness 至少需要：

- 输入样本
- 期望输出或评分规则
- 被测系统版本
- 模型和参数配置
- 运行日志
- 结果报告

Harness 的价值是可重复。没有可重复运行的 eval，你就很难比较不同 prompt、不同模型、不同检索策略。

> *Harness 是 eval 的"跑步机"——同一个样本、同一套评分、同一个环境，重复跑才能比较差异。没有可重复性，eval 结果就是一次性的。*


### Golden Set

Golden Set 是一组被认真挑选和标注的测试样本。

它不一定要很大。早期 30 到 100 条高质量样本，往往比一堆随便收集的问题更有用。关键是覆盖真实任务和关键失败模式。

Golden Set 应该包含：

- 常见正常问题
- 边界问题
- 容易误判的问题
- 高风险问题
- 历史 bug
- 用户真实反馈样本

每修一个重要 bug，都应该考虑把它变成 regression 样本。

> *Golden Set 的关键不是"大"而是"精"。30-100 条高质量样本覆盖正常、边界、高风险和历史 bug，比 1000 条随便收集的数据更有价值。每修一个 bug 就加一条 regression 样本——Golden Set 是长出来的，不是一次写完的。*


### LLM-as-Judge

LLM-as-Judge 是用模型来给模型输出评分。它适合评估开放式答案，比如摘要质量、是否回答完整、是否遵循格式、是否引用来源。

但它不能被神化。Judge 模型也会偏、会漏、会被输出风格影响。更稳的做法是：

- 对可自动判断的字段用规则评分。
- 对开放式质量用 LLM judge。
- 对高风险样本保留人工抽检。
- 定期校准 judge 和人工评分的一致性。

LLM-as-Judge 是评估工具，不是最终真相。

> *LLM-as-Judge 是"用 AI 评 AI"——方便但不绝对。规则能判的用规则，开放质量用 judge，高风险必须人工抽检。Judge 本身也需要校准。*


### Regression

Regression (回归) 是防止旧问题复发。

AI 应用很容易出现"修 A 坏 B"。一次 prompt 修改、一次模型升级、一次 retriever 调整，都可能影响很多旧场景。Regression set 的作用就是把历史问题固定下来，每次改动都重新跑。

一个实用做法：

1. 用户反馈一个错误。
2. 复现并记录输入。
3. 标注期望输出或拒答条件。
4. 加入 regression set。
5. 之后每次发布前跑一次。

> *Regression 是"不要让旧 bug 复活" -> 回归测试 。每次修 bug 的标准动作：复现 → 记录 → 加入 regression set → 以后每次发布前跑。这是 AI 应用的"免疫系统"。*


### Observability

Observability 是线上观察系统行为的能力。Eval 多数发生在发布前，observability 发生在真实使用中。

你至少要记录：

- 输入类型和来源
- 检索结果
- 工具调用
- 模型输出
- 错误和重试
- 用户反馈
- 成本和延迟

没有 observability，你就不知道真实用户在哪里失败，也不知道该往 golden set 里补什么。

> *Observability 是"线上的眼睛"。Eval 发现已知问题，observability 发现未知问题。没有线上数据，你不知道用户在哪里失败，Golden Set 也不知道该补什么。*

## 在 AI x Web3 中的位置

AI x Web3 系统里，eval 更重要，因为错误可能影响资产、权限、治理判断和链上执行。

需要特别评估：

- 交易解释是否准确
- 风险提示是否漏报
- 工具调用参数是否越界
- 是否能拒绝不确定请求
- 是否能识别 Prompt Injection
- 引用和来源是否可追溯
- 高风险动作是否要求 human check

Eval 不会替代交易模拟和权限控制，但它能让你持续发现系统在什么场景下不可靠。

> *在 AI×Web3 里，eval 的风险更高——错了不是"答错题"，而是"转错账"。交易解释、风险提示、工具调用参数这些场景必须有 eval 守住。*

## 扩展阅读

- [OpenAI Evals API Reference](https://platform.openai.com/docs/guides/evals)：查看 OpenAI 平台如何创建和运行 eval
- [OpenAI: How evals drive the next chapter in AI](https://openai.com/index/how-evals-drive-the-next-chapter-in-ai/)：从产品和业务角度理解 eval 为什么重要
- [OpenAI Evals GitHub](https://github.com/openai/evals)：开源 eval 框架和样例，适合理解 benchmark / grader 的组织方式
- [LangSmith Evaluation Docs](https://docs.smith.langchain.com/evaluation)：了解 LLM 应用的 dataset、experiment、feedback 和 tracing
- [RAGAS Documentation](https://docs.ragas.io/)：适合学习 RAG 场景下的回答质量、上下文相关性和 faithfulness 评估


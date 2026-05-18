# 最小实践：结构化摘要格式微调前评估

> 来源：Fine-tuning 模块 · 练习类型：微调决策评估

## 目标

在决定是否 fine-tune 之前，用 eval 对比三种方案的效果差异。重点不是"要不要微调"，而是"微调是不是必要的"。

## 样本准备

先准备 50 条样本：

- 输入：一段技术文档或提案
- 输出：固定 JSON 字段，例如 `summary`、`risks`、`open_questions`、`sources`

## 三种方案对比

### 方案 A：只改 Prompt

用不同的 prompt 表达同样的任务要求。

### 方案 B：Prompt + Few-shot

在 prompt 中加入 2-3 个示例。

### 方案 C：小规模 Fine-tuning 或 Adapter

用 50 条样本做 SFT 或 LoRA 微调。

## 评估维度

每种方案都用同一套 eval 检查：

- 字段是否完整
- 是否编造来源
- 风险点是否漏掉
- 输出是否稳定（同一输入多次运行结果一致）

## 决策原则

只有当前两种方案无法稳定解决问题时，再考虑 fine-tuning。

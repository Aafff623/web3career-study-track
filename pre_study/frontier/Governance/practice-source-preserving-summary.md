# Practice: 来源保真治理摘要

> 模块：前沿探索 · Governance

## 目标

为一个真实 DAO 提案做一份来源保真的治理摘要，确保每个关键事实都能追溯到来源。

## 场景

Optimism Collective 的一个 Retro Funding 提案：资助公共物品开发者工具项目。

## 流程

### 1. 提案摘要

```markdown
# 提案摘要：Retro Funding #4 — 开发者工具轮

## 结论
本提案为 Retro Funding #4 分配 800 万 OP 资助开发者工具类公共物品项目。

## 背景
Retro Funding 是 Optimism Collective 的追溯性公共物品资助机制。
本轮聚焦开发者工具：合约模板、测试框架、文档工具、安全分析。
[来源：Optimism Governance Forum, 2026-04-15]

## 预算
- 总额：8,000,000 OP
- 付款资产：OP token
- 付款方式：milestone-based escrow
[来源：提案文档 Section 3]

## 支持理由
- 开发者工具降低新项目进入门槛
- 历史数据显示工具类项目 ROI 较高
- 社区投票通过率 >70%
[来源：Forum 讨论, 多个 badgeholder 发言]

## 反对理由
- 预算分配缺乏明确评分标准
- 部分工具项目已获其他资助
- badgeholder 参与率偏低可能影响代表性
[来源：Forum 讨论, 反对方发言]

## 未回答问题
- 评分标准具体是什么？
- 如何避免重复资助？
- badgeholder 投票率数据？

## 执行动作
- 提案通过后 7 天内启动申请窗口
- 申请期 30 天
- badgeholder 评审 14 天
- 资助发放后按 milestone 释放
```

### 2. 来源保真检查

| 关键事实 | 来源 | 类型 | 可验证 |
|---------|------|------|--------|
| 预算 800 万 OP | 提案文档 Section 3 | 官方文档 | ✅ |
| 聚焦开发者工具 | 提案文档 Section 1 | 官方文档 | ✅ |
| 付款方式 milestone escrow | 提案文档 Section 4 | 官方文档 | ✅ |
| 社区投票率 >70% | Forum 统计 | 链下数据 | ⚠️ 需验证 |
| badgeholder 参与率偏低 | Forum 讨论 | 推断 | ⚠️ 需更多证据 |

### 3. 不确定性标注

- "社区投票率 >70%" — 来自 Forum 统计，需确认具体数据源
- "badgeholder 参与率偏低" — 来自多个发言者的观察，非官方统计
- "评分标准不明确" — AI 推断，基于提案文档未找到明确标准

### 4. 反方观点保留

- 方案 A（匿名 badgeholder）：担心代表性不足
- 方案 B（公开 badgeholder）：担心被游说
- AI 不做判断，只呈现两方论点

### 5. 审计字段

```json
{
  "event": "governance_summary",
  "proposal_id": "optimism-retro-funding-4",
  "facts_count": 8,
  "sources_attached": 8,
  "uncertainties_flagged": 2,
  "counter_arguments_preserved": 2,
  "ai_disclaimer_included": true,
  "timestamp": "2026-05-20T10:30:00Z"
}
```

## 验收标准

- [ ] 至少 5 个关键事实附来源链接
- [ ] 事实与推断明确分离
- [ ] 保留至少 2 个反方观点
- [ ] 标注不确定性内容
- [ ] 包含 AI 说明（不代表投票建议）

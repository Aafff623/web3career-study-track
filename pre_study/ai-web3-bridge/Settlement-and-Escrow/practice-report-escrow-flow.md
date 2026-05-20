# Practice: Agent 付费生成报告 Escrow 流程

> 模块：AI × Web3 交叉 · Settlement-and-Escrow

## 目标

设计一个"Agent 委托服务方生成报告"的完整 escrow 流程，覆盖资金锁定 → 交付 → 验收 → 释放 / 退款 / 争议。

## 场景

用户让 Agent 花 2 USDC 购买一份合约风险分析报告，服务方承诺 10 分钟内交付。

## 流程

1. 定义 escrow 状态机：Created → Funded → Delivered → Accepted → Released（异常：Refunded / Disputed）
2. 定义资金锁定：用户 → escrow 合约 2 USDC
3. 定义交付证明：IPFS hash 或文件 hash + 时间戳
4. 定义验收条件：报告包含指定字段（风险项数量、合约地址、漏洞分类）
5. 定义 evaluator：脚本检查字段完整性 + AI 检查语义质量
6. 定义退款规则：超时 10 分钟未交付 → 自动退款；交付不合格 → challenge window 48 小时
7. 定义争议流程：双方提交证据 → 多签仲裁 → 裁决后 24 小时可申诉

## 验收标准

- [ ] 状态机 ≥ 6 个状态，覆盖正常 + 异常
- [ ] 交付证明与任务 ID 绑定
- [ ] 验收条件可检查（非纯主观）
- [ ] evaluator 有版本记录
- [ ] 退款规则包含部分交付场景
- [ ] 争议流程有发起成本 + 证据格式 + 裁决权 + 申诉路径

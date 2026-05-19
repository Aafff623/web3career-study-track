# 实践：交易安全检查表

> 模块：Web3 基础 · Security · 状态：✅

## 目标

以一笔真实的合约调用交易为样本，逐项拆解其安全要素，建立从"交易阅读"到"Agent 安全执行"的检查清单。


## 流程

1. 在 Etherscan 或区块浏览器上找到一笔公开的合约调用交易（优先选择涉及 token transfer、权限变更或合约升级的交易）。
2. 记录基础信息：from、to、method signature、value、block number、gas used、status。
3. 展开 token transfers，列出所有涉及的 token、金额、转出方和接收方。
4. 展开 event logs，判断这笔交易是否触发了权限变更（如 ownership transfer、role grant）、资产参数变更（如 fee 调整、oracle 更新）或合约升级。
5. 评估风险等级：低（普通 transfer）/ 中（带参数变更的调用）/ 高（权限或合约变更），并说明判断依据。
6. 假设这笔交易由 AI Agent 发起，列出执行前必须完成的 simulation 检查项（如资产变化预览、revert 预测、gas 估算、授权额度校验）。
7. 假设这笔交易由 AI Agent 发起，列出需要 human check 的条件（如金额超过阈值、涉及权限变更、目标合约不在白名单）。
8. 写出上线后应监控的 event 或异常指标（如大额转出、非常规 method 调用、连续失败交易、TVL 异常波动）。
9. 总结：从这笔交易中学到了什么安全检查习惯，哪些步骤可以固化为 Agent 的 policy 规则。


## 验收标准

- [ ] 记录了一笔真实交易的完整基础信息
- [ ] 列出了所有 token transfers 和 event logs
- [ ] 判断了交易的风险等级并给出依据
- [ ] 写出了 Agent 发起时的 simulation 检查清单
- [ ] 写出了 human check 触发条件
- [ ] 写出了上线后监控指标
- [ ] 总结了可固化为 Agent policy 的安全规则

# 17 小时最全 Web3 教程 — ERC20 / NFT / Hardhat / CCIP 跨链

> Bilibili Web3 极客社区出品的 Web3 开发系列课程。本目录沉淀课程笔记（biliGPT 提取 + 人工清洗），用于跟做实操、回溯最佳实践。

## 课程来源

- **Bilibili 视频系列**：[BV1RFsfe5Ek5](https://www.bilibili.com/video/BV1RFsfe5Ek5)
- **BibiGPT 提取**：[bibigpt.co/video/BV1RFsfe5Ek5](https://bibigpt.co/video/BV1RFsfe5Ek5)
- **总时长**：约 17 小时（系列总览）

## 课程结构

```
ERC20 / FundMe 众筹 → Solidity 基础 → Hardhat 测试 → ERC721 NFT → CCIP 跨链
       ↓
合约语法 → 工厂模式 → 单元/集成测试 → NFT 实操 → 跨链验证
```

## 笔记索引

| # | 主题 | 状态 | 笔记 |
|---|------|------|------|
| 1 | （未拉取） | ⚪ | _暂无_ |
| 2 | Solidity 基础 — Hello World | ✅ | [`02-solidity-hello-world.md`](./02-solidity-hello-world.md) |
| 3 | Solidity 进阶 — FundMe & ERC-20 | ✅ | [`03-fundme-erc20.md`](./03-fundme-erc20.md) |
| 4 | （未拉取） | ⚪ | _暂无_ |
| 5 | Hardhat 开发框架 — 合约测试 | ✅ | [`05-hardhat-testing.md`](./05-hardhat-testing.md) |
| 6 | 跨链应用 — CCIP | ✅ | [`06-ccip-cross-chain.md`](./06-ccip-cross-chain.md) |
| 7 | 接下来做什么 | ✅ | [`07-next-steps.md`](./07-next-steps.md) |

## 学习记录

- **2026-05-23**：5 课笔记入库（biliGPT 清洗版），跟做实操尚未启动
- **2026-05-24**：参考代码克隆入 [`code/`](./code/) — 来源 [smartcontractkit/Web3_tutorial_Chinese](https://github.com/smartcontractkit/Web3_tutorial_Chinese)，已剥离 `.git`，主仓库通过 [`./.gitignore`](./.gitignore) 排除该目录
- **TODO**：第 1 课 / 第 4 课笔记待补；跟做实操可基于 `code/` 起步，产出落到 [`hackathon/`](../../../hackathon/) 或独立 practice 目录

## 笔记规范

- 每节课一份 `.md`，命名 `<序号>-<英文 slug>.md`（如 `02-solidity-hello-world.md`）
- 顶部 YAML frontmatter 含 `type / source / lesson / cleaned_at / tags`
- 内容遵循 [`toolkit/workflows/livestream-note-pipeline.md`](../../../toolkit/workflows/livestream-note-pipeline.md)：保留原文表述，仅修格式 + 错别字

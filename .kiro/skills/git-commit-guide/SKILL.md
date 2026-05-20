---
name: git-commit-guide
description: |
  Git 提交规范化指引。当用户说"提交一下"、"commit"、"帮我写 commit"时，按此规范生成 commit message。
  覆盖全部 type 定义、scope 规则、subject 风格和 body 格式。
---

# Git Commit Guide Skill

项目 git 提交的统一规范。Agent 生成 commit message 时必须遵循此规范，用户也可手动参考。

## Commit 格式

```
<type>(<scope>): <subject>

<body（可选）>
```

- `type`：提交类型（见下方）
- `scope`：可选，影响范围（日期 / 模块名 / 模块缩写）
- `subject`：简短描述，中英文均可，不超过 72 字
- `body`：可选，补充信息（Tx Hash、关联 issue 等）

## Type 类型

### 常规（贯穿全程）

| type | 用途 | 频率 |
|------|------|------|
| `log` | 每日学习笔记、Co-Learning 记录、daily-log 维护 | 每天 |
| `task` | 任务完成、打卡提交、交付证明 | 按需 |
| `study` | 预习资料整理、知识笔记（含笔记 + 实践文件） | 预习阶段高频 |
| `docs` | README、规范文件、索引、文档更新 | 按需 |
| `chore` | 仓库结构调整、配置变更、目录维护 | 按需 |

### 进阶（Skill / 重构 / 打磨）

| type | 用途 | 频率 |
|------|------|------|
| `refactor` | 重构已有内容：Skill 迭代、架构调整、工作流优化 | Skill 迭代时 |
| `polish` | 打磨 / 润色：README 美化、格式规范化、视觉调整 | 按需 |

### Hackathon 阶段（Week 3-4）

| type | 用途 | 频率 |
|------|------|------|
| `feat` | Hackathon 项目新功能 | Week 3-4 高频 |
| `fix` | Bug 修复 | Week 3-4 |
| `contract` | 智能合约相关（部署、测试、验证、交互） | Week 3-4 |

### 特殊

| type | 用途 | 频率 |
|------|------|------|
| `init` | 项目 / 目录 / 模块初始化 | 仅一次 |

## Scope 规则

- **日期**：`MM-DD` 格式，如 `05-18`，不写年份
- **模块名**：直接写模块名或缩写，如 `web3`、`skills`、`readme`、`cascade-maintain`
- **可省略**：当 subject 已经足够清晰时，scope 可以不写

## Subject 风格

- 不超过 **72 字**（git log 默认换行宽度）
- 中英文混排，技术术语保留英文
- 用 `—`（em dash）连接主信息和补充信息
- 信息结构：**做了什么 + 结果/规模**

## Body 格式

当有 Tx Hash 时必须附在 body：

```
contract(06-10): 部署 SessionKey 合约到 Sepolia

Tx Hash: 0x1234...abcd
Network: Sepolia
Contract: 0xabcd...1234
```

Skill 迭代时建议附带经验摘要：

```
refactor(skills): 经验沉淀 — N 条教训迭代到 skill-name

1. 教训一
2. 教训二

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>
```

## 实际示例

```bash
# 每日笔记（最高频）
log(05-18): AI Agent 入门课程笔记
log(05-20): Frontier 模块 6 节全部完成 — 笔记 + 实践 + 级联同步

# 预习资料
study(LLM): 整理大语言模型预习笔记
study(web3): 完成 Web3 基础 10 节预习笔记 + 练习文件

# Skill 迭代
refactor(skills): 经验沉淀 — 7 条实战教训迭代到 pre-study-note + cascade-maintain

# README / 文档
docs(readme): 用户微调 — 标题、描述、章节命名优化
polish(readme): 规范化微调 + readme-polish skill 沉淀到全局

# Hackathon（Week 3-4）
feat: 初始化 Agent Wallet 项目结构
contract: 部署 SessionKey 合约到 Sepolia
fix: 修复 Gas 估算逻辑

# 项目初始化
init: project structure for AI Web3 School BootCamp study track
```

## 规则

1. **一天可以多次提交**，按内容类型分开（笔记一次、任务一次、维护一次）
2. **不要把多天的内容合成一个 commit** — git log 就是你的学习时间线
3. **每个 commit 只做一件事** — 不要把笔记更新和目录调整混在一起
4. **Co-Authored-By**：Agent 协助完成的 commit 附带 `Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>`
5. **不要自动 push** — commit 后等用户确认再 push

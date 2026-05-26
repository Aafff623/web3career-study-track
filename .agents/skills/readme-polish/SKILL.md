---
name: readme-polish
description: |
  项目 README 规范化生成与打磨。基于代码事实审计功能声明，按统一视觉规范（徽章语义、Mermaid 色板、章节命名、引用块标注）输出可信、清晰、适合展示的项目入口。支持从零创建和基于已有 README 迭代两种模式。Use when 用户说"帮我写 README"、"打磨一下 README"、"生成项目首页"、"优化 README"，或任何涉及 README.md / 项目首页 / 仓库入口文档创建、重写、迭代的场景。即使 README 已经存在，只要用户提到优化、打磨、调整排版、加徽章、加架构图，也应触发。
---

# README Polish

> 不是营销式吹项目，而是基于代码事实，把 README 打磨成**可信、清晰、适合展示**的项目入口。

## 目标与原则

1. **事实优先**：每个已实现功能声明，都必须能在代码、配置、文档、示例或测试中找到依据。
2. **找不到依据的内容**，只能放到 Roadmap / Planned，不要写成已实现。
3. **不要直接重写全文**，先输出结构方案等用户确认。
4. **语气**：中英混排、有观点不煽情、专业可信、拒绝 AI 味营销腔。

## 触发判断

用户输入包含以下任一意图时，执行本 skill：

- "帮我写 README" / "生成项目首页" / "初始化 README"
- "打磨一下 README" / "优化 README" / "调整 README"
- "加徽章" / "加架构图" / "加 Banner" / "改排版"
- 涉及 README.md 的创建、重写、迭代、视觉升级

## 执行流程

### Step 1 · 项目事实扫描

读取以下文件，总结项目定位：

- `README.md`（已有则审计，无则从零）
- `package.json` / `pom.xml` / `build.gradle` / `pyproject.toml`（如有）
- `src/` / `docs/` / `examples/` / `tests/` / `assets/`（如有）
- 纯文档仓库：额外扫描 `__index__.md` / `WEEK.md` / `TASK.md` 等结构文件

输出：**项目事实摘要**（定位、技术栈、核心模块、运行方式）

### Step 2 · Claim Audit

列出现有 README 的所有功能声明，标注证据状态：

| 状态 | 含义 |
|------|------|
| `verified` | 有代码/配置/文档/测试依据 |
| `outdated` | 曾正确，但项目已变更 |
| `partial` | 部分正确，需补充或修正 |
| `planned` | 规划中，尚未实现 |
| `unsupported` | 找不到任何依据 |

输出：**Claim Audit 表**

### Step 3 · 定位确认

先问用户 README 面向谁：

- **面试官** — 突出学习轨迹、工程化思维、技术深度
- **比赛评委** — 突出项目价值、可演示性、链上证明
- **开源开发者** — 突出复用性、文档完整性、贡献入口
- **普通用户** — 突出 Quick Start、使用场景、截图演示
- **商业客户** — 突出解决方案、ROI、案例验证

默认假设：**比赛评委 + 面试官**（学习营项目性质）

### Step 4 · 信息架构设计

基于审计结果和定位，输出 README 大纲：

```
# Project Name
## Header（标题 + 描述 + Banner + Badges + 导航锚点）
## ✨ Highlights（亮点聚焦，3-5 条核心主张）
## 🌱 Origin / Motivation（起源与动机，可选）
## 📊 Progress / Status（当前进度，动态更新）
## 📂 Repo Structure（仓库结构，文字 + Mermaid）
## ⚙️ Workflow / Architecture（工作流或架构，Mermaid 图）
## 💡 Key Insights（核心判断/技术观点，引用块 + 斜体）
## 🏆 Hackathon / Roadmap（方向或路线图）
## 🔗 Links（关键链接）
## 🔒 Privacy / License（隐私提醒或协议）
## 🤝 Thanks / Credits（鸣谢，可选）
```

> 不要机械套用。根据项目类型增删：代码项目加 Quick Start / Usage；纯文档项目加学习路径 / 每日索引。

### Step 5 · 视觉与表达

按 [references/conventions.md](references/conventions.md) 执行：

- **Banner**：如适合，生成 Banner Prompt（风格、尺寸、内容要素）
- **Badges**：shields.io，按语义配色（蓝=信息，绿=完成，橙=进行中，红=警告）
- **Mermaid**：架构图 / 流程图 / 时间线，按色板显式 style 每个节点
- **引用块 + 斜体**：技术观点、判断、核心结论用 `> *内容*` 格式
- **图片穿插**：关键节点配图（进度截图、架构图、演示 GIF），居中 + alt 文本

### Step 6 · 用户确认与生成

1. 展示结构方案 + Claim Audit + 风格建议
2. 等用户确认或调整
3. 确认后生成最终 README.md

## 视觉规范速查

| 元素 | 规范 |
|------|------|
| Header | 标题 → 描述 → Banner(100%宽) → Badges(for-the-badge) → 导航锚点(·分隔)，全部居中 |
| 徽章语义 | 蓝=周期/信息，亮绿=完成/状态，橙=进行中/待定，红=警告/阻塞 |
| 章节标题 | `## emoji English (中文)`，二级 `###` 不加 emoji |
| Mermaid 色板 | 紫(#6C3CE1)=工具/起点，蓝(#3B82F6)=辅助，黄(#F59E0B)=进行中(文字#000)，绿(#10B981)=产出/完成，红(#EF4444)=里程碑/危险 |
| 引用块 | 技术观点/判断用 `> *斜体内容*`，核心结论用 `> **粗体内容**` |
| 代码/工具 | 反引号包裹，如 `Claude Code`、`.claude/skills/` |
| 中英混排 | 英文术语前后留空格，如 "Agent 编排"、"README Polish" |

## 输出要求

每次执行必须输出：

1. **项目事实摘要**
2. **Claim Audit 表**
3. **README 大纲**
4. **风格建议**（Badge / Mermaid / Banner / 图片）
5. **需要用户确认的问题**

用户确认后，再生成最终 README.md 全文。

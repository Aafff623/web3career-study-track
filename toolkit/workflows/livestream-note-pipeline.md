---
name: livestream-note-pipeline
type: workflow
added: 2026-05-23
tags: [biligpt, daily-log, livestream, cleanup]
---

# 直播录播笔记沉淀工作流

> 把 Bilibili 上的直播录播，经 biliGPT 自动提取后，沉淀为带规范的每日学习笔记。
> 解决问题：录播视频不便检索，手记又过于耗时；biliGPT 自动产出虽快但格式 / 错别字时有问题。

## 适用场景

- 主办方直播课程 / Co-Learning / Workshop 录播
- 任何"听过但没及时记下来"的视频内容
- 需要把视频核心点沉淀到 [`daily-log/`](../../daily-log/) 的每日笔记里时

## 流程

```
biliGPT 生成原始 .md/.html  →  复制进 repo  →  清洗格式  →  修错别字  →  入库 + 引用  →  Review  →  Commit
       (本地)                   (临时区)         (保留原意)    (轻改不破坏)     (跨文件链接)    (人审)    (规范)
```

### Step 1 · 源文件准备

biliGPT 产出 `.md` 或 `.html`，存在本机指定文件夹。

将文件复制到目标 daily 目录的临时位置（或 Agent 直接读取本地路径处理后写入），不要在原始路径修改。

### Step 2 · 清洗格式

**保留原始内容**，只动渲染/结构层。允许的操作：

- 移除导出工具自带的页眉 / 页脚 / "由 X 生成"水印
- 修复错位的 Markdown 语法：未闭合的代码块、奇数个反引号、错位的列表缩进
- 表格列对齐 / 多余的空白行（连续 3+ 空行压成 1 行）
- HTML 渲染产物（`&nbsp;`、`<br>` 等）转回 Markdown 等价形式
- 时间戳格式统一（如有）：`[mm:ss]` 或 `[hh:mm:ss]`

**禁止的操作**：

- 改写表述、重组段落顺序、删合"看起来重复"的内容 —— biliGPT 提取的语义是原始证据
- 跨段落"优化"逻辑 —— 把作者意图改成 Agent 的理解
- 用自己的话替换原意 —— 笔记是"嘉宾说过什么"，不是"我理解的是什么"

### Step 3 · 修正错别字

仅修正明显的同音字 / 拼写错误，限于：

- 中文同音错字（"原码 → 源码"、"借鉴 → 借鉴"）
- 英文术语拼写（"smart contact → smart contract"）
- 标点中英混用导致的渲染问题

修正后若改动多于 5 处，文末加一行：
```
> *清洗说明：修正错别字 N 处、格式问题 M 处，未改写表述。*
```

### Step 4 · 入库 + 引用

文件落到：

```
daily-log/week-N/YYYY-MM-DD/meetings/<slug>.md
```

`<slug>` 用英文短横线命名，与直播主题对应（如 `open-agentic-economy.md`、`ai-web3-basics.md`）。

文件头加 YAML 元数据：

```yaml
---
type: livestream-note
date: YYYY-MM-DD
week: N
source:
  platform: bilibili
  url: https://www.bilibili.com/video/<bvid>
  duration: HH:MM:SS
extracted_by: biliGPT
cleaned_at: YYYY-MM-DD
---
```

然后在两个地方反向引用：

1. **当日 TASK.md**：在对应直播任务的"产出"列添加链接
2. **当日 `YYYY-MM-DD.md`**：在"今天做了什么"或"产出与检验"提到直播时，加链接到 `meetings/<slug>.md`

### Step 5 · Review 提醒

Agent 清洗完成后，**必须**主动提醒用户进行 review。提醒内容包含：

- 涉及哪几个文件（路径列表）
- 清洗动作摘要（修了 N 处错别字、M 处格式问题）
- 是否触发"未改写表述"的边界（如有疑义的句子保留 + 标注）

用户回复 OK 后再进入 Step 6。

### Step 6 · Commit

按 [git-commit-guide](../../.claude/skills/git-commit-guide/SKILL.md) 规范，每场直播一个 commit：

```
log(<MM-DD>): <slug> 直播笔记沉淀 — N 章节 / biliGPT 清洗
```

多场同日直播也分开 commit，便于回溯。

## 注意事项

- 不污染原始数据：本地 biliGPT 输出文件夹不动，repo 里是清洗后副本
- 单一来源原则：每场直播只对应一个 `meetings/<slug>.md`，多份原始输出（如有多个版本）合并时优先取最新一份，旧版本可保留为 `<slug>.v1.md`
- 文件命名冲突：同日多场直播用不同 slug 区分，不堆在同一文件
- 不要把直播主题里的中文直接当文件名 —— Windows / Mac / Linux 行为不一致
- 历史课程的 5/18 等扁平 `meeting-*.md` 已迁移到本约定（见 GUIDE.md 决策记录）

## 与已有规范的关系

- 文件位置约定：见 [`GUIDE.md`](../../GUIDE.md) "直播录播笔记规范"节
- 批注格式：复用预习笔记批注规范（`> *批注*`）
- 提交规范：见 [git-commit-guide](../../.claude/skills/git-commit-guide/SKILL.md)

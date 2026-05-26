# README 视觉与语义规范

> 本文件为 readme-polish skill 的参考规范。执行 polish 时按此标准检查并输出。

---

## 1. Header 结构

全部居中，自上而下：

```markdown
<p align="center">
  <h1 align="center">Project Name · 中文副标题</h1>
  <p align="center"><strong>一句话描述项目核心价值的标语</strong></p>
</p>

<p align="center">
  <img src="assets/banner.png" alt="Banner" width="100%">
</p>

<p align="center">
  <img src="shields-badge-blue" alt="周期">
  <img src="shields-badge-green" alt="进度">
  <img src="shields-badge-orange" alt="状态">
</p>

<p align="center">
  <a href="#-highlights">Highlights</a> · <a href="#-progress">Progress</a> · ...
</p>
```

- Banner 图宽度 `100%`，放在 `assets/banner.png` 或 `assets/banner.svg`
- Badge 使用 `shields.io`，风格 `?style=for-the-badge`
- 导航锚点用 `·` 分隔，链接到各章节

---

## 2. 徽章配色语义

| 颜色 | 含义 | 用途 |
|------|------|------|
| **蓝色 `#007EC6`** | 信息 / 周期 | 营期时间、版本号、协议类型 |
| **亮绿 `#4C1`** | 完成 / 状态 | 进度百分比、已完成标记、CI 通过 |
| **橙色 `#FE7D37`** | 进行中 / 待定 | Hackathon 方向待定、开发中功能 |
| **红色 `#E05D44`** | 警告 / 阻塞 | 安全提醒、未开始、已知问题 |
| **灰色 `#9F9F9F`** | 未开始 / 备用 | 占位状态、计划中的模块 |

> 避免一个 README 里同语义用不同颜色。进度条和状态徽章必须保持一致。

---

## 3. 章节命名

一级标题格式：

```markdown
## emoji English-Name (中文名)
```

- emoji 放最前，作为视觉锚点
- 英文名首字母大写，kebab-case 或自然词组
- 中文名括号包裹
- 例外：过长英文名可直接用中文，如 `## 📊 当前进度`

二级标题不加 emoji：

```markdown
### 子章节标题
```

---

## 4. Mermaid 色板

所有 Mermaid 节点必须显式 `style`，禁止使用默认色：

| 颜色 | 语义 | 使用场景 |
|------|------|----------|
| `#6C3CE1` 紫 | 工具 / 起点 / 输入 | 外部工具、原始数据、起点节点 |
| `#3B82F6` 蓝 | 辅助 / 中间处理 | 转换、过滤、中间层 |
| `#F59E0B` 黄 | Skill / 进行中 | 正在执行的阶段、Agent 处理（文字 `#000`） |
| `#10B981` 绿 | 产出 / 完成 | 最终结果、已完成的模块、输出物 |
| `#EF4444` 红 | 里程碑 / 危险 / 决策点 | 关键节点、风险提醒、必须人工确认的点 |

```mermaid
graph LR
    A["输入"] --> B["处理"] --> C["产出"]
    style A fill:#6C3CE1,color:#fff
    style B fill:#F59E0B,color:#000
    style C fill:#10B981,color:#fff
```

---

## 5. 语气与排版

### 中英混排
- 英文术语前后留空格：`Agent 编排`、`README Polish`、`Smart Contract`
- 代码/工具名用反引号：`Claude Code`、`.claude/skills/`、`wcb-sync`
- 避免全大写缩写堆砌，首次出现写全称

### 强调层级
- **粗体** = 核心结论、关键数据、必须记住的点
- *斜体* = 补充说明、背景信息、引用来源
- `代码块` = 命令、文件名、配置键、短代码片段
- > 引用块 = 观点、判断、警示、个人反思

### 引用块 + 斜体标注（精髓设计点）

技术观点、核心判断、学习感悟使用：

```markdown
> *Agent 不应该拥有"钱包"，它应该只拥有 **可限制、可审计、可撤销** 的能力。*
```

效果：

> *Agent 不应该拥有"钱包"，它应该只拥有 **可限制、可审计、可撤销** 的能力。*

适用场景：
- 架构设计原则
- 技术选型理由
- 学习过程中的关键顿悟
- 对某个概念的个人理解

---

## 6. 图片穿插规范

### 位置策略
- **Banner**：Header 区，唯一全宽大图
- **进度截图**：Progress 节，展示完成状态
- **架构图**：Workflow / Architecture 节，Mermaid 为主，复杂场景可配静态图
- **演示 GIF**：Highlights 或 Usage 节，展示交互效果

### 格式要求
```markdown
<p align="center">
  <img src="assets/xxx.png" alt="描述文字" width="80%">
</p>
```

- 非 Banner 图宽度建议 `80%`，避免顶天立地
- 必须写 `alt` 文本，描述图片内容
- 截图配简短说明文字，放在图上方或下方

---

## 7. Banner 设计

### 尺寸
- 宽屏推荐：`1920×400` 或 `1600×320`
- 适配 `width="100%"`，高度自适应

### 内容要素
- 项目名称（大字）
- 一句话 slogan
- 视觉符号（与项目主题相关：如 AI × Web3 可用神经网络 + 区块链节点融合图形）
- 背景色或渐变（深色底 + 亮色文字更耐看）

### 生成 Prompt 模板

```
生成一张项目 Banner 图。
主题：[AI × Web3 / 数据工具 / 开源项目等]
风格：科技感、深色背景、简洁现代
尺寸：1920×400
内容：项目名称"XXX" + 标语"YYY" + 相关视觉符号
配色：[参考 Mermaid 色板，主色紫/蓝/绿]
文字：清晰可读，无衬线字体
```

---

## 8. 常见反模式

| 反模式 | 正确做法 |
|--------|----------|
| " revolutionary " " groundbreaking " 营销词 | 用具体事实替代："42 节预习完成"而非"海量学习" |
| Badge 颜色混乱 | 同语义固定一种颜色 |
| Mermaid 默认灰节点 | 全部显式 style |
| 章节无 emoji 或 emoji 过多 | 一级标题 1 个，二级不加 |
| 图片无 alt 文本 | 每张图写描述性 alt |
| 中英混排无空格 | `AI Agent` 而非 `AIAgent` |
| README 写成产品宣传页 | 基于代码事实，未实现的放 Roadmap |

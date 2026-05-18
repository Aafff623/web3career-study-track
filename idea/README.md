# idea ｜ 实验性构思

> 存放工作流中沉淀的可复用模式、skill 原型和待验证的想法。

## 定位

这个目录不是正式产出，而是"想法的草稿本"。当我在日常 workflow 中发现重复模式、可抽象的流程、值得做成 skill/slash command 的经验，就先记在这里。

## 目录结构

```
idea/
├── README.md              # 本文件
├── skills/                # 可复用的 skill（SKILL.md 格式）
│   ├── pre-study-note/    # 预习笔记整理
│   └── daily-log-sync/    # 每日日志同步
├── reference/             # 参考资料
│   ├── case/              # 经典案例（输入→输出对照）
│   └── eval/              # 进化规范（评估标准、断言、评分）
└── workflows/             # 可固化的 workflow 模式
```

## 什么该放进来

- 重复出现的 workflow 模式（比如"每次整理笔记都是同样的步骤"）
- 可以抽象成 slash command 的经验
- 待验证的工具组合方案
- 项目结构 / 规范的优化想法
- Hackathon 方向的早期灵感

## 什么不该放进来

- 正式的项目文档（放对应模块目录）
- 临时的 debug 记录（放 daily-log）
- 已经落地的规范（放 GUIDE.md / CLAUDE.md）

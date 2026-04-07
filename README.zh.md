# RepoAtlas

**给 AI agent 一张项目地图，而不是一本 1000 页的说明书。**

[English](README.md)

---

## 为什么存在

和编程 agent 协作时，常见痛点是：**上下文窗口短**、**没有持久记忆**：每次新对话都是冷启动。模型会忘记上周定下的决策、踩过的坑、以及团队约定的「当前焦点」。同样的约束你要反复讲一遍又一遍。

**RepoAtlas 给仓库配一套记忆系统**——不是聊天记录，而是**编译进仓库**的知识：一张精简的项目地图、决策记录、错题本、任务状态与追加式日志。agent 在工作过程中**增量更新**这一层，后续会话能接上上次的结论，而不是从零重新摸索。

- **已有（存量）项目：** **无侵入**地加入挽具——不改业务代码。拷贝 `AGENTS.md`、`project-memory/`，并把框架内容合并进 `docs/`。执行首次引导（`docs/agent/FIRST_RUN.md`）即可启动。不是重写项目，而是给 agent 一个可长期维护的「记忆位」。
- **新建（从零）项目：** 第一天就把同样文件拷进去，让记忆层随代码一起生长。

不需要数据库。不需要向量服务。不需要任何基础设施。只有 markdown 文件和一套清晰的协议。

---

## 问题

每次你和 AI 编程助手开启新对话，它都从零开始。重新阅读代码、重新发现架构、重新学习你上周已经教过它的教训。没有积累。知识在每次会话中被重新推导，而不是被编译。

## 解决方案

RepoAtlas 把 **"编译，而非检索"** 的模式应用到代码工程中。agent 不再把每次会话当作对仓库的一次全新 RAG 查询，而是增量地构建和维护一个持久的知识层——结构化的、交叉链接的、始终保持最新的。

agent 做记账的苦活。你做工程。

---

## 工作原理

### 三层结构

```
┌─────────────────────────────────────────┐
│  原始材料层                              │
│  代码、测试、配置、docs/raw/            │
│  （不可变 — agent 只读不改）            │
├─────────────────────────────────────────┤
│  策划文档层                              │
│  docs/architecture/                     │
│  docs/decisions/                        │
│  docs/modules/                          │
│  （长期维护、agent 维护）                │
├─────────────────────────────────────────┤
│  动态记忆层                              │
│  project-memory/                        │
│  当前焦点、任务、教训、日志              │
│  （热状态、频繁更新）                    │
└─────────────────────────────────────────┘
```

### 三种操作

| 操作 | 作用 | 何时 |
|------|------|------|
| **Ingest（编译）** | 从源材料提取持久知识，更新记忆与文档 | 有意义的代码变更、调试、设计讨论之后 |
| **Query（加载）** | 按任务分层加载刚好够用的上下文 | 每次会话、每个任务 |
| **Lint（健康检查）** | 检查记忆是否过期、矛盾、孤儿文档 | 大改之后，或怀疑漂移时 |

---

## 快速开始

### 1. 放进你的项目

把框架文件复制到你现有的仓库中：

```bash
git clone https://github.com/Jinbo666/RepoAtlas
cp -r RepoAtlas/{AGENTS.md,docs,project-memory} /path/to/your/project/
```

对**应用代码与配置**而言是无侵入的：你会增加 `AGENTS.md`、`project-memory/`，以及在 `docs/` 下的框架内容。

**若你已有 `docs/` 目录：**很多项目本身就有 `docs/`。本框架使用 `docs/agent/`、`docs/architecture/`、`docs/decisions/`、`docs/modules/`、`docs/raw/` 等子路径。把本仓库 **`docs/` 里的内容拷贝或合并**进你工程即可，不必覆盖你原有文档；只要这些子目录存在即可。

### 2. 首次运行

告诉你的 AI agent：

> 阅读 `docs/agent/FIRST_RUN.md` 并初始化项目。

就这样。agent 会自动扫描仓库结构、分类源代码根目录、创建项目地图、初始化记忆层。

### 3. 日常使用

初始化之后，直接开始工作。agent 在每次会话开始时读取 `AGENTS.md`，它会被路由到当前焦点、活跃任务和架构概览。agent 只加载需要的内容，然后尽早停止。不会有 1000 页的上下文倾泻。

### 4. 喂入原始文档

有设计文档、会议记录、研究笔记、遗留规格说明、踩坑记录？放到：

```
docs/raw/
```

框架把 `docs/raw/` 视为**不可变的源材料**。agent 只读不改。当你让 agent 处理一份原始文档时，它会提取持久价值的知识，编译进相应的策划文档和记忆文件——就像往 wiki 里导入一个新的信息源。

---

## 随时间积累的产物

| 产物 | 文件 | 说明 |
|------|------|------|
| 项目地图 | `source-roots.md`, `system-overview.md`, `module-graph.md` | 仓库结构、模块关系、入口点 |
| 决策史 | `docs/decisions/DEC-*.md` | 上下文、备选方案、理由、后果 |
| 错题本 | `recent-lessons.md` | 根因、预防规则、毕业生命周期 |
| 当前状态 | `current-focus.md` | 优先级、风险、下一步行动 |
| 会话日志 | `log.md` | 时间戳记录的变更和原因 |

每条教训有生命周期：`active` → `cooling` → `graduated`（升入架构/决策文档）或 `retired`。知识持续积累，但热层始终精简。

---

## 目录结构

```
your-project/
├── AGENTS.md                          # 入口 — 地图（约 70 行内）
├── docs/
│   ├── raw/                           # 原始材料（不可变）
│   ├── agent/
│   │   ├── FIRST_RUN.md               # 首次引导
│   │   ├── index.md                   # agent 操作文档导航
│   │   ├── context-loading.md         # 分层加载上下文
│   │   ├── memory-update-policy.md    # 何时、编译什么
│   │   ├── lint-and-health.md         # 健康检查协议
│   │   └── templates/                 # 模板
│   │       ├── decision-note.md
│   │       ├── lesson-note.md
│   │       ├── module-note.md
│   │       ├── session-note.md
│   │       └── task-note.md
│   ├── architecture/                  # 系统形状（首次运行后生成）
│   ├── decisions/                     # 长期技术决策
│   └── modules/                       # 模块边界说明
└── project-memory/
    ├── current-focus.md               # 仪表盘：优先级、风险、下一步
    ├── tasks/
    │   ├── active.md
    │   ├── backlog.md
    │   └── done.md
    ├── recent-lessons.md              # 热层错题本
    ├── log.md                         # 时间线日志
    ├── index.md                       # 记忆导航索引
    ├── source-roots.md                # 仓库根分类
    └── source-registry.md             # 原始文档登记
```

---

## 兼容性

适用于任何能读 markdown 文件的 AI 编程 agent：Cursor、Claude Code、OpenAI Codex、Windsurf，或任何能读仓库文件的 agent。

无供应商锁定。就是 markdown。

---

## 灵感来源

- **[LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** — Andrej Karpathy 提出的模式：让 LLM 构建并维护一个持久的、不断积累的知识库，而不是每次查询都从头推导。RepoAtlas 把这个模式从个人知识管理迁移到了代码工程。

- **[Harness Engineering](https://openai.com/zh-Hans-CN/index/harness-engineering/)** — OpenAI 提出的实践：为 AI agent 构建结构化的工程挽具（AGENTS.md、文档、规范），让它们有效地参与真实代码库的工作。RepoAtlas 提供了一个即用型的挽具起步模板。

---

## License

MIT

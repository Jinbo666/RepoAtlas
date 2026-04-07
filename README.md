# RepoAtlas

**Give your AI agent a map of the project, not a 1000-page manual.**

RepoAtlas is a lightweight, repo-native framework that turns your codebase into an agent-readable system of record. Drop it into any project — the AI agent compiles and maintains a persistent project memory layer: a living map, a decision history, a pitfall notebook, and a current-state dashboard.

No database. No embedding server. No infrastructure. Just markdown files and a clear protocol.

[English](#how-it-works) | [中文](#工作原理)

---

## The Problem

Every time you start a new chat with an AI coding agent, it starts from zero. It re-reads your code, re-discovers your architecture, and re-learns the lessons you already taught it last week. There's no accumulation. Knowledge is re-derived on every session, never compiled.

## The Solution

RepoAtlas applies the **"compile, don't retrieve"** pattern to code engineering. Instead of treating each session as a fresh RAG query over your repo, the agent incrementally builds and maintains a persistent knowledge layer — structured, interlinked, and always current.

The agent does the bookkeeping. You do the engineering.

---

## How It Works

### Three Layers

```
┌─────────────────────────────────────────┐
│  Raw Source Layer                        │
│  code, tests, configs, docs/raw/        │
│  (immutable — agent reads, never edits) │
├─────────────────────────────────────────┤
│  Curated Docs Layer                     │
│  docs/architecture/                     │
│  docs/decisions/                        │
│  docs/modules/                          │
│  (long-lived, agent-maintained)         │
├─────────────────────────────────────────┤
│  Dynamic Memory Layer                   │
│  project-memory/                       │
│  current-focus, tasks, lessons, log     │
│  (hot state, frequently updated)        │
└─────────────────────────────────────────┘
```

### Three Operations

| Operation | What it does | When |
|-----------|-------------|------|
| **Ingest** | Agent reads sources, extracts durable knowledge, updates affected memory/docs | After meaningful code changes, debugging sessions, design discussions |
| **Query** | Agent loads just enough context for the current task via layered reading profiles | Every session start, every task |
| **Lint** | Agent health-checks the memory layer for staleness, contradictions, orphan docs | After heavy changes, or when drift is suspected |

---

## Quick Start

### 1. Add to your project

Copy or clone this framework into your existing repository:

```bash
# Option A: Clone and copy
git clone https://github.com/Jinbo666/RepoAtlas
cp -r RepoAtlas/{AGENTS.md,docs,project-memory} /path/to/your/project/

# Option B: Use as a template on GitHub
# Click "Use this template" on the repo page
```

It is **non-invasive** for application code and configs: you add `AGENTS.md`, `project-memory/`, and the framework files under `docs/`.

**If you already have a `docs/` folder:** many projects already use `docs/` for their own documentation. RepoAtlas uses conventional subpaths such as `docs/agent/`, `docs/architecture/`, `docs/decisions/`, `docs/modules/`, and `docs/raw/`. Simply **copy or merge** this repository’s `docs/` contents into your project’s `docs/`—no need to replace your existing docs; only these subfolders are required for the harness.

### 2. First Run

Tell your AI agent:

> Read `docs/agent/FIRST_RUN.md` and initialize the project.

That's it. The agent will:

1. Scan your repository structure
2. Classify source roots (code, tests, configs, raw docs)
3. Create a thin project map (architecture overview, module graph, invariants)
4. Initialize the memory layer (current focus, task scaffold, log)
5. Write a bootstrap log entry

### 3. Normal Work

After initialization, just start working. The agent reads `AGENTS.md` at the start of each session, which routes it to:

1. `project-memory/current-focus.md` — what matters now
2. `project-memory/tasks/active.md` — what's in progress
3. `docs/architecture/system-overview.md` — how the system works

The agent loads only what it needs and stops early. No 1000-page context dump.

### 4. Feed Your Raw Docs

Have design docs, meeting notes, research notes, legacy specs, or pitfall writeups? Drop them into:

```
docs/raw/
```

The framework treats `docs/raw/` as **immutable source material**. The agent reads from it but never modifies it. When you tell the agent to process a raw doc, it extracts durable knowledge and compiles it into the appropriate curated docs and memory files — just like ingesting a new source into a wiki.

---

## What Gets Built Over Time

As you work with the agent across sessions, the memory layer accumulates:

- **Project Map** — `source-roots.md`, `system-overview.md`, `module-graph.md`
- **Decision History** — `docs/decisions/DEC-0001-*.md` with context, alternatives, rationale
- **Pitfall Notebook** — `recent-lessons.md` with root cause, prevention rules, graduation lifecycle
- **Current State** — `current-focus.md` with priorities, risks, next actions
- **Session Log** — `log.md` with timestamped entries of what changed and why

Each lesson has a lifecycle: `active` → `cooling` → `graduated` (into architecture/decisions) or `retired`. The knowledge compounds, but the hot layer stays lean.

---

## File Structure

```
your-project/
├── AGENTS.md                          # Entry point — the map (< 70 lines)
├── docs/
│   ├── raw/                           # Your raw source documents (immutable)
│   ├── agent/
│   │   ├── FIRST_RUN.md               # First-time bootstrap guide
│   │   ├── index.md                   # Agent operation docs navigation
│   │   ├── context-loading.md         # How to load just enough context
│   │   ├── memory-update-policy.md    # When and what to compile
│   │   ├── lint-and-health.md         # Health check protocol
│   │   └── templates/                 # Reusable templates
│   │       ├── decision-note.md
│   │       ├── lesson-note.md
│   │       ├── module-note.md
│   │       ├── session-note.md
│   │       └── task-note.md
│   ├── architecture/                  # System shape (generated on first run)
│   ├── decisions/                     # Durable technical decisions
│   └── modules/                       # Module boundary docs
└── project-memory/
    ├── current-focus.md               # Dashboard — priorities, risks, next actions
    ├── tasks/
    │   ├── active.md                  # Current work
    │   ├── backlog.md                 # Not yet started
    │   └── done.md                    # Completed
    ├── recent-lessons.md              # Hot-layer pitfall notebook
    ├── log.md                         # Chronological update log
    ├── index.md                       # Memory navigation index
    ├── source-roots.md                # Repository root classification
    └── source-registry.md             # Raw doc processing tracker
```

---

## Compatibility

Works with any AI coding agent that reads markdown files:

- [Cursor](https://cursor.sh) — reads `AGENTS.md` as workspace rules
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — reads `AGENTS.md` as project context
- [OpenAI Codex](https://openai.com/index/openai-codex/) — reads `AGENTS.md` as agent instructions
- [Windsurf](https://windsurf.com) — reads `AGENTS.md` as project rules
- Any agent that can read files from the repo

No vendor lock-in. It's just markdown.

---

## Inspiration

This project is inspired by two key ideas:

- **[LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** by Andrej Karpathy — the pattern of having LLMs build and maintain a persistent, compounding knowledge base instead of re-deriving knowledge from scratch on every query. RepoAtlas adapts this from personal knowledge management to code engineering: the "wiki" becomes a project memory layer; "ingest" becomes compilation of code changes, debugging lessons, and design decisions; "lint" becomes truth maintenance against the living codebase.

- **[Harness Engineering](https://openai.com/zh-Hans-CN/index/harness-engineering/)** by OpenAI — the practice of building structured harnesses (AGENTS.md, docs, conventions) that give AI agents the context they need to work effectively on real codebases. RepoAtlas provides a ready-made harness starter that any project can adopt.

---

## License

MIT

---

<a id="工作原理"></a>

# RepoAtlas（中文）

**给 AI agent 一张项目地图，而不是一本 1000 页的说明书。**

RepoAtlas 是一个轻量级的、仓库原生的框架，把你的代码仓库变成一个 agent 可读的系统。把它放进任何项目里——AI agent 会编译并维护一个持久的项目记忆层：一张活的地图、一部决策史、一本错题本、一个当前状态仪表盘。

不需要数据库。不需要向量服务。不需要任何基础设施。只有 markdown 文件和一套清晰的协议。

---

## 问题

每次你和 AI 编程助手开启新对话，它都从零开始。重新阅读代码、重新发现架构、重新学习你上周已经教过它的教训。没有积累。知识在每次会话中被重新推导，而不是被编译。

## 解决方案

RepoAtlas 把 **"编译，而非检索"** 的模式应用到代码工程中。agent 不再把每次会话当作对仓库的一次全新 RAG 查询，而是增量地构建和维护一个持久的知识层——结构化的、交叉链接的、始终保持最新的。

agent 做记账的苦活。你做工程。

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

## 兼容性

适用于任何能读 markdown 文件的 AI 编程 agent：Cursor、Claude Code、OpenAI Codex、Windsurf，或任何能读仓库文件的 agent。

无供应商锁定。就是 markdown。

---

## 灵感来源

- **[LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** — Andrej Karpathy 提出的模式：让 LLM 构建并维护一个持久的、不断积累的知识库，而不是每次查询都从头推导。RepoAtlas 把这个模式从个人知识管理迁移到了代码工程："wiki"变成了项目记忆层；"ingest"变成了对代码变更、调试教训和设计决策的编译；"lint"变成了针对活代码库的真值维护。

- **[Harness Engineering](https://openai.com/zh-Hans-CN/index/harness-engineering/)** — OpenAI 提出的实践：为 AI agent 构建结构化的工程挽具（AGENTS.md、文档、规范），让它们有效地参与真实代码库的工作。RepoAtlas 提供了一个即用型的挽具起步模板。

---

## License

MIT

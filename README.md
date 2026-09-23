# cuin-skills

> 个人制作的 AI Agent Skills 合集 · A personal collection of AI Agent Skills

[中文](#中文) | [English](#english)

---

<a id="中文"></a>

## 中文

### 简介

本仓库用于集中存放我个人制作的 AI Agent Skill。所有 Skill 均为「指令式 Skill」：由 Markdown 文档构成，不包含可执行代码，也不依赖任何第三方库，可直接被支持 `SKILL.md` 约定的 Agent 读取使用。

随着制作的 Skill 增多，会按功能分类持续收录进本仓库。

### Features

- **零依赖**：纯 Markdown，无需安装运行时或第三方包
- **引擎/技术栈无关**：Skill 内不绑定具体框架、语言或项目
- **按功能分类**：统一放入分类目录，避免每个 Skill 各占一个顶层目录
- **结构完整**：每个 Skill 保持其独立文件夹与原始目录结构

### 已收录 Skill

当前共收录 **2** 个 Skill，全部属于 `development`（开发/编程类）。

#### development — 开发/编程类

| Skill | 说明 | 目录 |
|---|---|---|
| **game-dev-team** | 游戏开发团队多角色协作框架。模拟完整小型游戏开发团队（制作人 / 游戏策划 / 技术负责人 / 游戏程序员 / 关卡设计师 / UI-UX 与美术设计 / 技术美术 / QA / 构建发布共 9 个角色），覆盖「规划 → 设计 → 开发 → 测试 → 发布」闭环。包含角色选择矩阵、标准八步流程、10 条工作规则、7 类场景流程模板，并附引擎适配表（Unity / Godot / Unreal / 自研）与发布检查清单。 | [`development/game-dev-team`](development/game-dev-team) |
| **software-dev-team** | 通用软件开发团队多角色协作框架。7 个核心角色（Product Owner / Technical Lead / Developer / UI-UX Designer / QA / Security Reviewer / DevOps-Release Engineer）+ 按项目类型自动增加专家角色（Web / WebGL / 小程序 / 移动 App / 桌面 / AI 应用 / API 服务端 / CLI），覆盖「需求 → 设计 → 开发 → 审查 → 测试 → 安全 → 构建 → 发布」闭环。包含标准九步流程、12 条工作规则、8 类场景流程模板、小任务简化规则与发布检查清单。 | [`development/software-dev-team`](development/software-dev-team) |

### Skill 分类

分类按 Skill 的**实际功能**判定，并优先复用已有分类，不为单个 Skill 新建分类。

| 分类目录 | 说明 | 当前数量 |
|---|---|---|
| `development/` | 开发 / 编程类：开发流程、编码规范、架构、测试、工程协作 | 2 |
| `automation/` | 自动化类：批处理、定时任务、流程自动化 | 0 |
| `ai/` | AI / Agent 类：Prompt 工程、Agent 协作、模型应用 | 0 |
| `productivity/` | 效率工具类：文档、笔记、信息整理 | 0 |
| `design/` | 设计 / 创作类：视觉、图形、内容创作 | 0 |
| `other/` | 无法归入以上分类的内容 | 0 |

> 目录会在首次有 Skill 归入时才创建；上表列出的空分类为分类规划，不代表已存在对应目录。

### Project Structure

```text
cuin-skills/
├── README.md
├── .gitignore
└── development/                     # 分类目录：开发/编程类
    ├── game-dev-team/
    │   ├── SKILL.md                 # 主文件：角色矩阵、八步流程、工作规则
    │   └── references/
    │       ├── roles.md             # 9 个角色的详细职责卡
    │       └── workflows.md         # 流程详解、引擎适配、发布检查清单
    └── software-dev-team/
        ├── SKILL.md                 # 主文件：角色矩阵、九步流程、工作规则
        ├── assets/                  # 资源目录（当前为空，保留占位）
        ├── scripts/                 # 脚本目录（当前为空，保留占位）
        └── references/
            ├── roles.md             # 7 个核心角色 + 项目类型专家角色
            └── workflows.md         # 流程详解、场景模板、发布检查清单
```

### 单个 Skill 的结构约定

每个 Skill 是独立文件夹，至少包含一个 `SKILL.md`：

```text
<skill-name>/
├── SKILL.md          # 必填。YAML frontmatter：name / description，正文为 Skill 指令
├── references/       # 可选。详细参考文档
├── assets/           # 可选。素材
└── scripts/          # 可选。辅助脚本
```

`SKILL.md` 的 frontmatter 示例：

```yaml
---
name: skill-name
description: 一句话说明该 Skill 的能力与适用场景，供 Agent 判断何时加载。
---
```

### Requirements

- 无运行时依赖，无第三方包
- 使用环境需支持 `SKILL.md` 约定的 Agent Skill 机制

### Installation / Usage

将对应 Skill 文件夹整体复制到用户级 Skill 目录下即可（保留文件夹本身）：

```bash
# 用户级 Skill 目录（跨项目可用）
~/.workbuddy/skills/

# 以 game-dev-team 为例
cp -r development/game-dev-team ~/.workbuddy/skills/
```

安装后，Agent 会根据 `SKILL.md` 中 `description` 描述的适用场景自动加载对应 Skill。两个团队协作类 Skill 的区分：

- 处理**游戏项目**任务 → `game-dev-team`
- 处理**普通软件项目**任务（Web / 小程序 / 后端 / CLI / AI 应用等）→ `software-dev-team`

### 核心设计说明

两个 Skill 共享同一套设计思路，区别只在角色构成与流程步骤数：

| 维度 | game-dev-team | software-dev-team |
|---|---|---|
| 角色数 | 9 个固定角色 | 7 个核心角色 + 按项目类型自动增加专家角色 |
| 标准流程 | 八步 | 九步 |
| 工作规则 | 10 条 | 12 条 |
| 场景模板 | 7 类 | 8 类 |
| 适用对象 | 游戏项目（引擎无关） | 通用软件项目（技术栈无关） |

共同的设计要点：

1. **先选角色再动手**——每轮声明本轮激活的角色及原因，未激活的角色不参与讨论，避免形式主义
2. **按任务规模选流程**——大型功能走标准流程，小任务走简化流程（保留「读代码 → 实现 → 验证」三段硬核）
3. **工程纪律**——先读后改、根因优先、复用以先、验证后才算完成、禁止用硬编码或屏蔽报错伪装完成
4. **统一输出格式**——每轮结束输出固定的「本轮总结」结构，含已完成内容、验证结果、已知技术债与下一步
5. **闭环自检**——每轮对照闭环覆盖表检查缺口，缺口写入下一步建议

### 安全与隐私

本仓库在发布前已执行敏感信息审计，确认：

- 无 API Key、Token、密码、数据库凭证、SSH Key
- 无 `.env`、私有配置、云服务凭证
- 无用户名、邮箱、手机号等个人信息
- 无本机绝对路径（文档中的路径均写作 `~/.workbuddy/skills/` 等相对或通用形式）
- 无内网地址、私有服务器信息
- 无日志、缓存、临时文件与编译产物

仓库内无任何需要运行的可执行代码或脚本，因此不存在运行期凭证或动态密钥加载。若后续新增 Skill 中含示例配置，会以占位符或 `.env.example` 形式提供。

### Contributing

本仓库是个人 Skill 收藏，不主动接受外部贡献。若发现内容问题，欢迎提 Issue 指出。

### Roadmap

- 持续将新制作的 Skill 按同一套分类规则收录进本仓库
- 当某分类下 Skill 数量增多时，再考虑在该分类内进一步细分

### License

本仓库**尚未添加开源协议**。在未明确授权前，默认保留所有权利。

如需复用，建议先通过 Issue 联系作者。若你希望以宽松方式开放使用，可后续补入 MIT 协议。

---

<a id="english"></a>

## English

### Overview

This repository is a personal collection of AI Agent Skills. Every Skill here is an *instruction-only* Skill: it consists of Markdown documents, contains no executable code, and depends on no third-party libraries. It can be read directly by any agent that follows the `SKILL.md` convention.

As more Skills are created, they will be categorized and added to this repository.

### Features

- **Zero dependencies** — pure Markdown, no runtime or packages required
- **Engine / stack agnostic** — Skills are not bound to a specific framework, language, or project
- **Categorized by function** — grouped into category directories instead of one top-level directory per Skill
- **Structure preserved** — each Skill keeps its own folder and original internal layout

### Included Skills

Currently **2** Skills are included, all under the `development` category.

#### development

| Skill | Description | Path |
|---|---|---|
| **game-dev-team** | A multi-role collaboration framework for game development. Simulates a small full game team (Producer, Game Designer, Technical Lead, Gameplay Programmer, Level Designer, UI/UX & Art Designer, Technical Artist, QA, Build & Release — 9 roles) and covers the full *plan → design → develop → test → release* loop. Includes a role-selection matrix, an 8-step standard workflow, 10 working rules, 7 scenario templates, an engine adaptation table (Unity / Godot / Unreal / in-house), and a release checklist. | [`development/game-dev-team`](development/game-dev-team) |
| **software-dev-team** | A multi-role collaboration framework for general software development. 7 core roles (Product Owner, Technical Lead, Developer, UI/UX Designer, QA, Security Reviewer, DevOps/Release Engineer) plus specialist roles added automatically per project type (Web / WebGL / Mini Program / Mobile / Desktop / AI app / API & backend / CLI). Covers the *requirements → design → develop → review → test → security → build → release* loop, with a 9-step workflow, 12 working rules, 8 scenario templates, small-task simplification rules, and a release checklist. | [`development/software-dev-team`](development/software-dev-team) |

### Categories

Categories are decided by each Skill's **actual function**. Existing categories are reused whenever possible; a new category is never created for a single Skill.

| Directory | Scope | Count |
|---|---|---|
| `development/` | Development / programming: workflows, coding standards, architecture, testing, engineering collaboration | 2 |
| `automation/` | Automation: batch jobs, scheduled tasks, process automation | 0 |
| `ai/` | AI / Agent: prompt engineering, agent collaboration, model applications | 0 |
| `productivity/` | Productivity: documents, notes, information organization | 0 |
| `design/` | Design / creation: visual, graphics, content creation | 0 |
| `other/` | Anything that does not fit the categories above | 0 |

> A directory is created only when a Skill is first assigned to it. Empty categories in the table above are planned categories and do not imply the directory already exists.

### Project Structure

```text
cuin-skills/
├── README.md
├── .gitignore
└── development/                     # Category: development / programming
    ├── game-dev-team/
    │   ├── SKILL.md                 # Main file: role matrix, 8-step workflow, working rules
    │   └── references/
    │       ├── roles.md             # Detailed role cards for 9 roles
    │       └── workflows.md         # Workflow details, engine adaptation, release checklist
    └── software-dev-team/
        ├── SKILL.md                 # Main file: role matrix, 9-step workflow, working rules
        ├── assets/                  # Assets directory (currently empty, kept as placeholder)
        ├── scripts/                 # Scripts directory (currently empty, kept as placeholder)
        └── references/
            ├── roles.md             # 7 core roles + per-project-type specialist roles
            └── workflows.md         # Workflow details, scenario templates, release checklist
```

### Skill Layout Convention

Each Skill is a standalone folder containing at least a `SKILL.md`:

```text
<skill-name>/
├── SKILL.md          # Required. YAML frontmatter: name / description; body holds the instructions
├── references/       # Optional. Detailed reference documents
├── assets/           # Optional. Assets
└── scripts/          # Optional. Helper scripts
```

Example `SKILL.md` frontmatter:

```yaml
---
name: skill-name
description: One sentence describing what the Skill does and when it applies, so the agent can decide when to load it.
---
```

### Requirements

- No runtime dependencies and no third-party packages
- An environment that supports the `SKILL.md` Agent Skill convention

### Installation / Usage

Copy the Skill folder as a whole into the user-level Skills directory:

```bash
# User-level Skills directory (available across projects)
~/.workbuddy/skills/

# Example: game-dev-team
cp -r development/game-dev-team ~/.workbuddy/skills/
```

Once installed, the agent loads a Skill automatically based on the scenario described in its `description` field. To choose between the two team-collaboration Skills:

- **Game** projects → `game-dev-team`
- **General software** projects (Web / Mini Program / backend / CLI / AI app, etc.) → `software-dev-team`

### Design Notes

Both Skills follow the same design philosophy; they differ only in role composition and step count:

| Aspect | game-dev-team | software-dev-team |
|---|---|---|
| Roles | 9 fixed roles | 7 core roles + specialists added per project type |
| Standard workflow | 8 steps | 9 steps |
| Working rules | 10 | 12 |
| Scenario templates | 7 | 8 |
| Target | Game projects (engine agnostic) | General software projects (stack agnostic) |

Shared design points:

1. **Pick roles before acting** — each round declares which roles are active and why; inactive roles stay out of the discussion to avoid ceremony
2. **Match the process to task size** — full workflow for large features, a simplified one for small tasks (keeping the hard core: *read the code → implement → verify*)
3. **Engineering discipline** — read before changing, fix root causes, reuse before rebuilding, no claiming "done" without verification, and no faking completion via hardcoding or suppressed errors
4. **Consistent output format** — every round ends with a fixed "round summary": what was done, verification results, known debt, and next steps
5. **Closed-loop self-check** — each round is checked against a coverage table, with any gap recorded as a next step

### Security & Privacy

A sensitive-information audit was performed before publication. Confirmed:

- No API keys, tokens, passwords, or database credentials
- No `.env` files, private configuration, or cloud credentials
- No usernames, email addresses, or phone numbers
- No machine-specific absolute paths (documented paths use forms such as `~/.workbuddy/skills/`)
- No internal network addresses or private server details
- No logs, caches, temporary files, or build artifacts

The repository contains no executable code or scripts, so there are no runtime credentials or dynamically loaded secrets. If future Skills include sample configuration, it will be provided as placeholders or `.env.example`.

### Contributing

This is a personal collection and does not actively accept external contributions. If you spot a problem, feel free to open an issue.

### Roadmap

- Keep adding newly created Skills using the same classification rules
- Split a category further only once it holds enough Skills to justify it

### License

**No open-source license has been added yet.** Without an explicit grant, all rights are reserved.

If you would like to reuse any of this, please open an issue first. If you prefer to open it up permissively, an MIT license can be added later.

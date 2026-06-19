# Product Prototype Builder

一个面向 AI Agent 的产品原型工作流 Skill：把模糊的产品想法，逐步推进为**需求讨论 → 版本化 PRD → 单文件可交互 HTML 原型**。

适合产品经理、设计师、独立开发者，以及希望在 Cursor、Codex 等 AI 工具中标准化「从 0 到 1 做原型」流程的使用者。

**在线演示（轻量任务看板示例）：** [点击体验 demo.html](https://htmlpreview.github.io/?https://raw.githubusercontent.com/tieveto666-code/product-prototype-builder/main/demo.html)

## 解决什么问题

很多 AI 原型工具的问题是：

- 跳过需求澄清，直接生成不可用的 PRD 或静态页面
- 原型看起来完整，但按钮点不动、流程走不通
- 修改需求后覆盖旧版本，无法追溯

本 Skill 通过**三阶段门禁**和**版本化管理**，让 AI 更像一个会追问、会确认、会交付可体验原型的产品搭档。

## 工作流程

```mermaid
flowchart LR
    A[产品想法] --> B[阶段一：需求讨论]
    B -->|用户确认| C[阶段二：PRD 方案]
    C -->|用户确认| D[阶段三：HTML 原型]
    D --> E[版本化交付物]
```

| 阶段 | 产出 | 门禁 |
|------|------|------|
| 需求讨论 | `{需求名称}-讨论.md` | 用户确认「可以生成 PRD」 |
| 需求方案 | `v00N-{需求名称}-方案.md` | 用户确认「可以生成原型」 |
| HTML 原型 | `v00N-{原型名称}.html` | 按质量规范自检后交付 |

## 仓库结构

```text
product-prototype-builder/
├── README.md
├── demo.html                           # 在线演示入口（示例原型副本）
├── LICENSE
├── SKILL.md                            # Cursor / Codex Skill 主文件
├── agents/
│   └── openai.yaml                   # Codex Agent 配置（可选）
├── references/
│   ├── portable-prompt.md            # 跨工具通用提示词
│   └── prototype-quality.md          # 原型质量与验收规范
└── examples/
    └── demo-task-board/              # 脱敏示例：轻量任务看板
        ├── 01-discussions/
        ├── 02-specifications/
        └── 03-prototypes/
```

## 安装方式

### Cursor

**方式 A：全局 Skill（推荐）**

```bash
git clone https://github.com/tieveto666-code/product-prototype-builder.git
cp -R product-prototype-builder ~/.cursor/skills/
```

**方式 B：项目规则**

```bash
git clone https://github.com/tieveto666-code/product-prototype-builder.git
mkdir -p .cursor/rules
cp product-prototype-builder/references/portable-prompt.md .cursor/rules/product-prototype-builder.mdc
cp product-prototype-builder/references/prototype-quality.md .cursor/rules/prototype-quality.mdc
```

也可以直接将 `references/portable-prompt.md` 和 `references/prototype-quality.md` 的内容粘贴到 Cursor 的项目规则或 Agent 自定义指令中。

在 Agent 对话中可这样触发：

```text
使用 product-prototype-builder 和我讨论一个产品想法
```

### OpenAI Codex

```bash
cp -R product-prototype-builder ~/.codex/skills/
```

### 其他 AI 工具（通用 Prompt）

若工具不支持 Skill 目录，可将 `references/portable-prompt.md` 粘贴为：

- 系统提示词
- 项目规则（Project Rules）
- 自定义 Agent 指令

原型生成阶段建议同时引用 `references/prototype-quality.md`。

## 快速体验示例

本仓库包含一个完整脱敏示例：**轻量任务看板**。

| 步骤 | 内容 |
|------|------|
| 在线演示 | [demo.html 可交互原型](https://htmlpreview.github.io/?https://raw.githubusercontent.com/tieveto666-code/product-prototype-builder/main/demo.html) |
| 需求讨论 | `examples/demo-task-board/01-discussions/轻量任务看板-讨论.md` |
| PRD | `examples/demo-task-board/02-specifications/轻量任务看板/v001-轻量任务看板-方案.md` |
| 版本化原型 | `examples/demo-task-board/03-prototypes/轻量任务看板/v001-轻量任务看板.html` |

示例原型支持看板拖拽、任务增删改查、搜索筛选、统计视图和 `localStorage` 持久化。

> **说明：** GitHub 的 Raw 链接只能查看 HTML 源码，无法运行交互。请使用上方在线演示链接，或下载 / 克隆仓库后在本地用浏览器打开 `demo.html`。

## 核心特性

- **阶段门禁**：避免 AI 过早生成 PRD 或原型
- **版本化管理**：PRD 与原型按 `v001`、`v002` 递增，不覆盖历史版本
- **交互质量约束**：所有主要按钮必须可点击、有反馈；看板/表单/弹窗具备模拟逻辑
- **单文件交付**：HTML/CSS/JS 内联，浏览器直接打开，无需构建
- **跨工具迁移**：Skill + portable prompt 双轨支持

## 适用与不适用

**适合：**

- 产品早期探索、需求梳理、方案评审
- 需要可点击、可演示的 HTML 原型
- 希望沉淀可复用的 AI 产品工作流

**不适合：**

- 直接替代生产级前后端开发
- 需要真实登录、支付、数据库、API 集成的场景（需转为工程项目）

## 贡献与反馈

欢迎通过 Issue 或 Pull Request 提出改进建议。

## License

[MIT](./LICENSE)

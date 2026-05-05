---
name: openspec-project-bootstrap
description: 将任意仓库初始化或补齐为“官方 OpenSpec + 项目治理增强”工作流。只要用户提到 OpenSpec 初始化、spec-driven 工作流搭建、`openspec/config.yaml`、根级或包级 `AGENTS.md`、`apply` 后的 `review`、归档前知识沉淀，或希望把仓库流程整理成可复用的 OpenSpec 初始化包时，都应主动使用这个 skill，即使用户没有明确说“请用一个 skill 来做”。
compatibility: 需要对目标仓库有 shell 和文件编辑能力；当 OpenSpec CLI 已安装或可安装时效果最佳。
---

# OpenSpec 项目初始化

## 概览

使用这个 skill，为一个新仓库初始化 OpenSpec，或者把一个已有仓库补齐为“保留官方 OpenSpec 结构，同时具备更强项目治理能力”的形态。

目标不是用自定义流程替代 OpenSpec，而是在保留官方 `explore -> propose -> apply -> archive` 主干的前提下，把项目规则分层补到 `openspec/config.yaml`、根 `AGENTS.md`、包级 `AGENTS.md`，以及按需补充的 `openspec/CODEX_MANUAL.md`。

## 何时使用

只要用户有下面这些需求，就应使用这个 skill：

- 在仓库里初始化 OpenSpec
- 把仓库升级为 spec-driven 开发方式
- 新增或重写 `openspec/config.yaml`
- 统一根级或包级 `AGENTS.md`
- 在 `apply` 之后加入项目级 `review` 阶段
- 在保留官方 OpenSpec 结构的前提下增加更强的项目规则
- 把零散的仓库协作流程整理成可复用的 OpenSpec 初始化包

## 决策路径

1. 如果目标仓库还没有 OpenSpec：
   先执行官方初始化，再套用这个 skill 里的治理模板。

2. 如果目标仓库已经有官方 OpenSpec，但项目规则较弱：
   保留现有官方结构，补强 `config.yaml`、`AGENTS.md`、包级规则和提示词资源。

3. 如果目标仓库已经演化出较重的自定义流程或非标准结构：
   先尽量回归官方 OpenSpec 概念，再继续增加项目级指导。

## 执行流程

### 1. 先检查当前仓库状态

在开始改动前，始终先确认这些信息：

- 是否已经存在 `openspec/`
- 当前仓库是否已经在使用官方结构
- 项目类型、技术栈、主入口、目录布局分别是什么
- 哪些目录需要自己的 `AGENTS.md`
- 项目是否需要更严格的确认闸门，以及 `apply` 后的 `review` 阶段

如果现有规则之间有冲突，先总结冲突点，再决定是否批量改写文件。

### 2. 保留官方 OpenSpec 基线

如果 OpenSpec 缺失，优先执行：

```bash
openspec init --tools codex
```

不要发明新的主流程目录去替代 `openspec/`。
不要把 `review` 伪装成新的官方命令。
应把 `review` 视为位于 `apply` 和 `archive` 之间的项目治理补充层。

### 3. 补项目上下文和模板

使用 `assets/templates/` 中的模板来完善目标仓库：

- 将 `assets/templates/openspec-config.yaml.example` 合并到 `openspec/config.yaml`
- 将 `assets/templates/AGENTS.template.md` 合并到目标仓库根 `AGENTS.md`
- 用 `assets/templates/PACKAGE_AGENTS.template.md` 为关键目录生成包级 `AGENTS.md`
- 只有在项目治理较重时，才增加 `assets/templates/CODEX_MANUAL.template.md`
- 当项目希望每个 change 都有长期保留的 review 结果时，使用 `assets/templates/review.md.example`

`AGENTS.md` 里只保留长期有效的规则，不要写临时排障记录或一次性任务背景。

### 4. 建立治理流程

默认情况下，这个 skill 推动的项目治理链路是：

```text
explore -> propose -> apply -> review -> wait for user confirmation -> archive
```

关键约束：

- `review` 是项目补充阶段，不是伪装出来的官方命令
- `apply` 阶段如果环境支持，应显式使用 TDD 和验证类技能
- 只有在用户确认后，才进入 `archive`
- `archive` 前应把长期有效的知识沉淀到合适的文档层级

### 5. 复用提示词资源

需要某个阶段的结构化提示词时，使用 `assets/prompts/` 下的资源：

- `official-init.md`
- `augment-project-rules.md`
- `generate-package-agents.md`
- `explore-requirement.md`
- `create-change.md`
- `execute-apply.md`
- `review-after-apply.md`
- `archive-change.md`

这些提示词已经按实际仓库协作场景组织好，可直接复用，也可按项目情况轻量改写。

### 6. 最终交付

将这个 skill 应用到目标仓库后，输出中应始终说明：

- 创建或更新了哪些文件
- 哪些规则属于官方 OpenSpec 基线
- 哪些规则属于项目增强
- 哪些目录新增了包级 `AGENTS.md`
- 当前仓库是否启用了 `apply` 之后的 `review` 步骤
- 推荐的下一步是 `explore`、`propose`、`apply` 还是 `archive`

## 护栏规则

- 尽可能保留官方 `openspec/` 目录结构。
- 优先改造模板，不要另造一套平行框架。
- 根规则保持全局性，包规则保持局部性。
- 如果项目默认语言不是中文，只调整语言约束，不要改变治理结构。
- 如果项目很轻量，可以不加 `openspec/CODEX_MANUAL.md`，但仍建议至少保留根级和包级 `AGENTS.md`。

## 资源

### 参考资料

- `references/official-baseline-vs-project-rules.md`
  用于解释哪些是官方 OpenSpec 基线，哪些是项目叠加治理规则。
- `references/bootstrap-any-project.md`
  用于执行一个新项目或老项目的完整初始化落地步骤。

### 模板

- `assets/templates/AGENTS.template.md`
- `assets/templates/PACKAGE_AGENTS.template.md`
- `assets/templates/openspec-config.yaml.example`
- `assets/templates/CODEX_MANUAL.template.md`
- `assets/templates/review.md.example`

### 提示词

- `assets/prompts/official-init.md`
- `assets/prompts/augment-project-rules.md`
- `assets/prompts/generate-package-agents.md`
- `assets/prompts/explore-requirement.md`
- `assets/prompts/create-change.md`
- `assets/prompts/execute-apply.md`
- `assets/prompts/review-after-apply.md`
- `assets/prompts/archive-change.md`

## 示例请求

**示例 1**
输入：`给这个新仓库加 OpenSpec，但不要改掉官方结构。`

**示例 2**
输入：`这个老项目已经有 openspec 目录了，帮我补齐 config 和 AGENTS 规则。`

**示例 3**
输入：`把这个 monorepo 整理成可以长期复用的 OpenSpec 初始化模板。`

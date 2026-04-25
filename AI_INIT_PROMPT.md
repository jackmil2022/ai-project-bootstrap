# AI 项目初始化总控提示词

> 本文件给 AI 读取，用于把当前仓库初始化成一个适合长期协作的 AI 项目工作区。具体是否会被某个工具自动读取，取决于工具版本、设置和运行方式；如果你能看到本文件，请优先遵守它。

> `README.md` 是给用户看的入口说明，不是完整的初始化规范。不要再把整套 AI 初始化规则塞回 `README.md`；请把面向 AI 的长期初始化规则保留在本文件和后续生成的 `AGENTS.md` 中。

## 任务目标

你要把当前仓库初始化成一个可持续维护的 AI 协作项目。整体流程以 OpenSpec 的开发生命周期为骨架，但本项目做了明确定制：

- 生命周期主线使用 `onboard / analyze -> propose -> design -> spec -> tasks -> apply -> review -> archive`
- 生命周期文档内容统一使用中文，便于理解、讨论、维护和交接
- `AGENTS.md` 是项目知识沉淀的主入口，也是长期规则的唯一主仓
- 在落文档前、落文档后、归档前，必须暂停并向用户说明变更点、方案、风险和下一步，等待用户确认
- `apply` 阶段的写代码方式以 Superpowers 的工作方式为主
- 代码完成后，必须按 everything-claude-code 的审查方式进行严格 review
- 归档前，必须把本次 change 暴露出的长期有效经验、边界和约束沉淀到合适层级的 `AGENTS.md`

## 参考来源

以下仓库用于提供方法论和流程骨架，不用于整仓照搬：

- OpenSpec: [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)
- OpenSpec 示例规格: [openspec/specs/cli-list/spec.md](https://github.com/Fission-AI/OpenSpec/blob/main/openspec/specs/cli-list/spec.md)
- Superpowers: [obra/superpowers](https://github.com/obra/superpowers)
- everything-claude-code: [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code)

使用原则：

- OpenSpec 提供 spec-driven development 的生命周期骨架
- Superpowers 提供 planning、TDD、debugging、verification、subagent 等写代码方式
- everything-claude-code 提供 review、质量检查、安全和回归审查方式
- 只保留当前项目真正需要的最小子集，不要把上游仓库原样复制进项目
- 如果可以联网，优先查看上游内容，并在 `.ai/UPSTREAM.md` 记录来源 URL 与 commit SHA

## 全局硬约束

- 先分析，后写入
- 先汇报，后修改
- 先合并，后新增
- 默认不覆盖已有 `AGENTS.md`、`CLAUDE.md`、`.cursor/rules/`、`README*`、`docs/`
- 任何删除、重命名、覆盖现有文件的动作，都必须先停下来等用户确认
- 如果遇到冲突，先说明保留什么、补充什么、跳过什么，再继续
- 对不确定字段，宁可省略，也不要编造
- 不要把 `TODO`、`待补充`、`<<占位符>>` 原样写入最终文件
- 不要声称某个工具一定会自动读取某个文件；统一使用保守表述，例如“建议入口”“通常可用”“取决于工具版本和设置”
- 同一功能只保留一份主规格文档，避免多处重复维护
- 所有长期稳定的项目知识，最终都要写回对应层级的 `AGENTS.md`

## `AGENTS.md` 是知识主仓

本项目把 `AGENTS.md` 视为项目知识沉淀的唯一主仓。

执行规则：

- 如果根目录没有 `AGENTS.md`，先创建
- 如果已有 `AGENTS.md`，以最小化合并方式补充，不覆盖用户已有内容
- 如果其他文档中已经存在长期稳定的项目规则、模块边界、命令约定、维护注意事项，要搬运或合并到对应层级的 `AGENTS.md`
- 根级 `AGENTS.md` 负责全局规则
- 包级、模块级、子目录 `AGENTS.md` 负责局部边界和本地约束
- 查询项目规则时，先查当前目录和父目录最近的 `AGENTS.md`
- 更新项目规则时，也优先写回对应层级的 `AGENTS.md`

特别说明：

- `AGENTS.md` 记录的是长期有效的边界、规则、约束和经验
- 一次性讨论、临时方案、阶段性草稿、短期任务状态，不要写进 `AGENTS.md`

## 编码工具识别与桥接策略

在初始化前，先判断用户正在使用哪种编码工具，以及仓库里已经存在哪些工具入口文件。

常见识别信号：

- `AGENTS.md`、`.codex/`：通常说明项目已经考虑 Codex 或通用 AI 协作入口
- `CLAUDE.md`、`.claude/`：通常说明项目兼容 Claude Code
- `.cursor/rules/`：通常说明项目兼容 Cursor
- `.github/copilot-instructions.md`：通常说明项目兼容 GitHub Copilot
- 其他工具自己的约定文件：保留，但不要把它们当作长期知识的主仓

桥接原则：

- 首选主入口始终是对应层级的 `AGENTS.md`
- 如果工具支持自己的桥接文件，例如 `CLAUDE.md` 或 `.cursor/rules/ai-workflow.mdc`，这些文件应保持轻量，主要负责索引回 `AGENTS.md`
- 如果某个工具不直接支持 `AGENTS.md`，则保留该工具支持的文档格式，同时在 `AGENTS.md` 中建立索引关系，并在桥接文件中明确说明：
  - 项目规则主仓是 `AGENTS.md`
  - 查询规则时先查对应层级的 `AGENTS.md`
  - 更新规则时先更新对应层级的 `AGENTS.md`
  - 工具专属文件只做桥接和兼容，不做主知识库
- 如果现有桥接文件里已经有稳定规则，要把这些规则迁移或合并到 `AGENTS.md`，再把桥接文件改成索引入口

## 推荐目标结构

初始化完成后，项目通常应具备以下结构；是否全部创建，取决于当前仓库现状和用户确认结果：

```text
AGENTS.md
CLAUDE.md                            # 如适用，作为桥接文件
.cursor/
└── rules/
    └── ai-workflow.mdc             # 如适用，作为桥接文件

.ai/
├── README.md
├── UPSTREAM.md
├── docs/
│   └── specs/
├── skills/
│   ├── README.md
│   ├── using-project-skills/SKILL.md
│   ├── brainstorming/SKILL.md
│   ├── writing-plans/SKILL.md
│   ├── test-driven-development/SKILL.md
│   ├── requesting-code-review/SKILL.md
│   ├── receiving-code-review/SKILL.md
│   ├── systematic-debugging/SKILL.md
│   ├── verification-before-completion/SKILL.md
│   ├── subagent-driven-development/SKILL.md
│   └── dispatching-parallel-agents/SKILL.md
└── openspec/
    ├── README.md
    ├── templates/
    │   ├── proposal.md
    │   ├── design.md
    │   ├── spec.md
    │   └── tasks.md
    └── examples/
        └── cli-list/
            └── spec.md
```

约定说明：

- `AGENTS.md` 是共享主入口
- `.ai/openspec/` 放中文版、轻量化、本地化的 OpenSpec 工作流
- `.ai/skills/` 放以 Superpowers 思想为主的本地 skills
- `.ai/docs/specs/` 放设计、方案、规格等项目文档
- `CLAUDE.md`、`.cursor/rules/ai-workflow.mdc` 等文件只作为桥接入口，不重复维护主规则

## OpenSpec 生命周期（中文版，本项目定制）

以下流程使用 OpenSpec 的生命周期作为骨架，但增加了本项目自己的硬门禁和编码规范。

> 这里的 `propose / design / spec / tasks / apply / archive` 是生命周期阶段名，不要求工具一定存在同名命令；请按阶段语义执行，不要假设固定命令一定可用。

### 阶段 0：Onboard / Analyze

先做分析，不立刻写文件。

必须完成：

- 扫描项目结构、语言、框架、包管理器、构建方式、测试方式
- 判断是否是 monorepo，并识别 apps / packages / services / libs / modules
- 检查现有 AI 入口和桥接文件
- 确认当前工具更适合读取哪些文件，以及如何桥接到 `AGENTS.md`
- 判断哪些内容应该直接合并到 `AGENTS.md`
- 判断哪些目录需要包级或模块级 `AGENTS.md`

第一轮输出必须包含：

- 项目类型
- 技术栈
- monorepo 判断
- 当前检测到的编码工具线索
- 现有 AI 配置
- 现有文档结构
- 建议新增
- 建议合并
- 建议跳过
- 潜在冲突
- 计划创建的 skills
- 计划创建的 OpenSpec 中文文件
- `AGENTS.md` / 桥接文件处理策略

在用户明确确认之前，不要创建、修改或删除任何文件。

### 门禁 1：落文档前必须停下来确认

在写 `proposal / design / spec / tasks` 之前，必须暂停，并向用户说明：

- 这次 change 的目标
- 影响范围
- 关键变更点
- 涉及哪些目录、包、模块、接口或边界
- 存在真实权衡时，给出 2-3 个方案和推荐方案
- 哪些知识将沉淀到 `AGENTS.md`

只有在用户明确确认方向后，才能真正落文档。

### 阶段 1：Design / Spec / Tasks（中文化）

确认后，再进入文档阶段。

文档原则：

- 优先使用中文版、轻量化、本地化的 OpenSpec
- 文档内容用中文写，文件组织保持清晰
- 对于中高影响改动，优先补齐 `proposal.md`、`design.md`、`spec.md`、`tasks.md`
- 对于低风险小改动，可以走轻量路径，但仍需保证信息完整
- 同一功能只保留一份主规格文档，不要在多个目录重复维护
- 文档中要明确目标、非目标、影响范围、边界、风险、验证方式

### 门禁 2：文档落地后、写代码前必须再次确认

文档写完后，必须再次暂停，并向用户说明：

- 文档路径
- 本次变更的核心决策
- 与原方案相比做了哪些取舍
- 风险点和未决项
- 接下来准备进入的 `apply` 范围

只有在用户明确确认后，才能进入 `apply` 阶段写代码。

### 阶段 2：Apply（写代码以 Superpowers 为主）

`apply` 阶段严格按 Superpowers 的风格执行。默认优先级如下：

1. 先理解现有代码和上下文，再修改
2. 复杂任务先做 planning
3. 新功能、行为变更、bug 修复，优先采用 TDD
4. 遇到 bug、测试失败、异常行为，先做系统化 root cause 分析，再修复
5. 只做小步、可验证、可回退的改动
6. 不夹带“顺手重构”或无关改动
7. 工具支持子代理或并发代理时，只在边界清晰、彼此独立的任务上使用
8. 没有验证证据，不要声称完成

在本项目中，建议优先建设或使用以下本地 skills：

- `using-project-skills`
- `brainstorming`
- `writing-plans`
- `test-driven-development`
- `systematic-debugging`
- `subagent-driven-development`
- `dispatching-parallel-agents`
- `verification-before-completion`

如果某次任务明显不适合 TDD，必须明确说明原因，并给出替代验证方式。

### 阶段 3：Review（严格按 everything-claude-code 方式执行）

代码写完后，不允许直接宣布完成，必须先 review。

review 原则：

- 如果工具支持 reviewer、code-reviewer、language reviewer 或独立审查模式，优先使用
- 如果工具不支持独立 reviewer，也必须按相同的检查框架做自审
- 输出顺序必须是“先问题，后总结”
- 问题按严重度排序
- 审查重点优先看：
  - 功能正确性
  - 行为回归
  - 安全风险
  - 测试缺口
  - 边界处理
  - 过度设计
  - 可维护性
- 每个问题尽量给出文件位置、原因和修复建议
- 重要问题修复后，必须重新验证

如果 review 发现高风险问题，不要进入归档阶段。

### 门禁 3：归档前必须停下来确认

准备归档前，必须再次暂停，并向用户说明：

- 本次 change 实际改了什么
- 还有哪些未覆盖的风险或限制
- 准备归档哪些文档
- 准备把哪些长期有效经验写回哪些 `AGENTS.md`
- 准备提交哪些文件

只有在用户明确确认后，才能进入归档。

### 阶段 4：Archive / Learn / Commit

归档阶段不能只做文档收尾，还必须完成知识沉淀。

必须完成：

- 总结本次 change 遇到的问题、踩过的坑、关键取舍和边界
- 区分哪些内容是全局规则，哪些是包级规则，哪些是模块级规则
- 把长期稳定、未来还会复用的内容写回合适层级的 `AGENTS.md`
- 如果对应层级没有 `AGENTS.md`，先新建再沉淀
- 不把一次性状态、临时吐槽、短期 workaround 写进 `AGENTS.md`
- 完成归档后，再提交本次变更涉及的文件

提交要求：

- 提交范围应聚焦本次 change
- 先确认归档和沉淀动作完成，再提交
- 如果用户没有额外约束，提交说明应清楚表达本次 change 的主题

## 初始化时必须改造的 OpenSpec 规则

相对原始 OpenSpec，本项目明确增加以下约束：

- 原始 OpenSpec 强调流程轻量、可流动更新；本项目仍保留这种灵活性，但额外增加 3 个强制暂停点：
  - 落文档前
  - 文档落地后、写代码前
  - 归档前
- 这 3 个节点必须先把变更点、方案、风险和下一步告诉用户，并等待确认
- `apply` 阶段不以任意代码生成风格为准，而以 Superpowers 的 planning / TDD / debugging / verification 风格为准
- `review` 阶段不只做表面检查，而要按 everything-claude-code 的审查方式做严格问题导向 review
- `archive` 阶段不只结束当前 change，还必须把这次 change 产生的长期有效知识沉淀到对应层级的 `AGENTS.md`

## 文件合并与冲突处理规则

当仓库里已经存在相关文件时，按以下顺序处理：

1. 先保留用户已有内容
2. 如果主题一致，做最小化合并
3. 如果结构明显冲突，先输出差异摘要和处理建议，再等待确认
4. 如果桥接文件已有大量稳定规则，先迁移到 `AGENTS.md`，再把桥接文件收缩为索引入口
5. 不主动删除用户已有文件，除非用户明确要求

## 建议创建的本地 skills

为了让 `apply` 与 `review` 阶段稳定落地，建议把以下 skills 统一放在 `.ai/skills/`：

- `using-project-skills`
- `brainstorming`
- `writing-plans`
- `test-driven-development`
- `requesting-code-review`
- `receiving-code-review`
- `systematic-debugging`
- `verification-before-completion`
- `subagent-driven-development`
- `dispatching-parallel-agents`

这些 skills 应以中文书写，保持轻量，但方法论以 Superpowers 为主。

## 建议创建的 OpenSpec 中文文件

建议在 `.ai/openspec/` 中创建中文版、本地化的最小子集：

- `README.md`
- `templates/proposal.md`
- `templates/design.md`
- `templates/spec.md`
- `templates/tasks.md`
- `examples/cli-list/spec.md`

这些文件的内容要用中文表达，但保留 OpenSpec 的核心价值：

- 先对齐
- 再落文档
- 再实现
- 再审查
- 再验证
- 再归档
- 再沉淀长期知识

## 初次响应格式

当你第一次接手这个初始化任务时，先只做分析，输出以下结构，然后等待用户确认：

- 项目类型：
- 技术栈：
- monorepo：
- 当前检测到的编码工具：
- 现有 AI 配置：
- 现有文档结构：
- `AGENTS.md` 处理策略：
- 建议新增：
- 建议合并：
- 建议跳过：
- 潜在冲突：
- 计划创建的 skills：
- 计划创建的 OpenSpec 中文文件：

在用户明确确认前，不要创建、修改或删除任何文件。

## 完成后输出格式

完成初始化或某次 change 后，输出一份简洁但完整的结果总结，至少包含：

1. 创建了哪些文件
2. 更新了哪些文件
3. 跳过了哪些文件，以及为什么
4. 当前项目规则主仓是哪些 `AGENTS.md`
5. 哪些桥接文件被保留，它们如何索引到 `AGENTS.md`
6. OpenSpec 中文版目录是什么
7. 本次 `apply` 采用了哪些 Superpowers 风格约束
8. 本次 `review` 如何按 everything-claude-code 执行
9. 归档前沉淀了哪些长期知识，分别写到了哪些 `AGENTS.md`
10. 如果参考了上游仓库，来源记录写到了哪里

## 最后的执行提醒

- 不要把上游仓库整套搬进来
- 不要让桥接文件和 `AGENTS.md` 双向漂移
- 不要在没有确认的情况下越过 3 个强制暂停点
- 不要在没有 review 和验证的情况下宣布完成
- 不要在归档时漏掉知识沉淀
- 不要忘记：查询规则和更新规则，都先看对应层级的 `AGENTS.md`

# AI Project Bootstrap

这是一个给人看的仓库入口，用来说明这个项目的用途，以及应该让 AI 去读哪份初始化提示词。

如果你是用户：

- 这个仓库的核心不是代码模板，而是一套“把任意项目初始化成 AI 可长期协作工作区”的提示词
- 这套提示词以 OpenSpec 生命周期为骨架
- 写代码阶段以 Superpowers 的方法论为主
- 代码完成后的 review 以 everything-claude-code 的审查方式为主
- 项目的长期知识主仓是 `AGENTS.md`

如果你是 AI：

- 不要把本 `README.md` 当成完整初始化规范
- 请先阅读 [AI_INIT_PROMPT.md](./AI_INIT_PROMPT.md)
- 再按其中的分析、确认、落文档、`apply`、`review`、`archive` 流程执行

## 这个仓库解决什么问题

很多 AI 编码工具支持的入口文件不同，知识又容易散落在 `README.md`、`CLAUDE.md`、`.cursor/rules/` 等多个位置。本仓库的目标是提供一套更稳定的初始化方式：

- 用 OpenSpec 生命周期组织需求、方案、实现、验证和归档
- 用 `AGENTS.md` 作为项目知识沉淀主仓
- 用轻量桥接文件兼容不同 AI 编码工具
- 用中文文档降低理解和维护成本

## 推荐使用方式

1. 把这个仓库放进你要初始化的项目里，或参考它的结构改造现有项目。
2. 在你的 AI 编码工具里，明确让 AI 先阅读 `AI_INIT_PROMPT.md`。
3. 让 AI 先分析当前项目，并在改文件前给出初始化计划。
4. 你确认后，再让 AI 开始创建或合并 `AGENTS.md`、`.ai/openspec/`、`.ai/skills/` 和桥接文件。
5. 在后续每次 change 中，继续按同一套流程执行。

如果你的工具不能直接读取仓库里的 Markdown 文件，通常可以手动把 `AI_INIT_PROMPT.md` 的内容粘贴给 AI 作为项目初始化提示词。

## 初始化后通常会得到什么

初始化完成后，项目通常会形成这些关键部分：

- `AGENTS.md`：项目知识主仓，记录长期有效的规则、边界和维护约定
- `.ai/openspec/`：中文版、轻量化、本地化的 OpenSpec 生命周期文档
- `.ai/skills/`：以 Superpowers 思想为主的本地 skills
- `CLAUDE.md`、`.cursor/rules/ai-workflow.mdc` 等桥接文件：如适用，用来兼容具体工具，但不作为主知识库

## 文件说明

- [README.md](./README.md)：给用户看的入口说明
- [AI_INIT_PROMPT.md](./AI_INIT_PROMPT.md)：给 AI 读取的初始化提示词

## 参考项目

- [OpenSpec](https://github.com/Fission-AI/OpenSpec)
- [Superpowers](https://github.com/obra/superpowers)
- [everything-claude-code](https://github.com/affaan-m/everything-claude-code)

## 一句话用法

可以直接对 AI 说：

```text
请先阅读项目根目录的 AI_INIT_PROMPT.md，先分析当前项目并给出初始化计划；在我确认前，不要改任何文件。
```

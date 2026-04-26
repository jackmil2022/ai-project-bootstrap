# 官方 OpenSpec 基线 vs 本项目规则

下面这份对比，重点不是判断谁“更正确”，而是告诉你哪些属于官方基础能力，哪些属于本项目后来叠加的治理规则。

## 一句话结论

- 官方 OpenSpec 更像一套轻量规范框架：先初始化，再围绕 `explore / propose / apply / archive` 工作。
- 本项目是在官方框架上，加了“中文化、双确认闸门、apply 后自动 review、review 后等待确认、archive 前知识沉淀、归档后 Git 跟进”这些强治理约束。
- 如果你要把这套经验迁移到任意项目，最稳妥的做法不是复制来源项目里可能存在的自定义 schema 或命令，而是保留官方 `spec-driven`，再通过 `config.yaml + 根/包级 AGENTS.md + 项目手册 + 提示词` 叠加项目规则。

## 对比表

| 维度 | 官方 / 常见基线 | 本项目现状 | 推荐迁移方式 |
| --- | --- | --- | --- |
| 初始化方式 | `openspec init --tools codex` | 在官方初始化之上补项目手册、中文输出约束、项目规则模板 | 先官方初始化，再补项目模板 |
| 目录结构 | `openspec/config.yaml`、`openspec/changes/`、`openspec/specs/`、`openspec/changes/archive/` | 额外维护 `openspec/CODEX_MANUAL.md`、根/包级 `AGENTS.md`、阶段化提示词 | 保留官方目录，项目补充规则单独承载 |
| 默认 schema | 官方实测为 `spec-driven` | 仍以官方 `spec-driven` 为基线，中文需求通过规则约束补足 | 任意项目先用官方 `spec-driven`，中文需求用规则约束补足 |
| 提示词分类 | `explore / propose / apply / archive` | 同样保留四类，但每类都叠加项目 override | 保留四类官方分组，不另造主命令 |
| explore 阶段 | 偏探索、偏思考，不强制产物 | 增加“第一确认闸门”，先确认再落 proposal/design/specs/tasks | 视项目治理强度决定是否继承 |
| propose 阶段 | 创建 change 和 artifacts | 项目要求先过第一确认闸门 | 建议迁移到新项目，尤其多人协作时 |
| apply 阶段 | 读上下文、按 tasks 实现 | 项目要求先过第二确认闸门；coding 阶段显式使用 `superpowers:test-driven-development`、`superpowers:requesting-code-review`、`superpowers:verification-before-completion`；apply 结束后自动进入 review | 建议迁移到新项目 |
| review 阶段 | 官方默认不单列为独立主命令 | 项目要求 apply 后自动进入 review，review 完成后先停下等待确认 | 作为项目治理补充保留，不伪装成官方命令 |
| archive 阶段 | 核对完成度、同步 specs、归档 change | 归档前先复盘并沉淀规则，用户要求 archive 时默认继续 Git 提交/推送 | 可迁移，但 Git 跟进建议按团队习惯开关 |
| 语言约束 | 官方默认英文文案更常见 | 项目默认中文输出与中文文档 | 用 `config.yaml` 和 `AGENTS.md` 指定 |
| 领域限制 | 官方不关心具体业务框架 | 项目会额外补主入口、目录职责、外部框架封装等专项约束 | 迁移时改成目标项目自己的边界 |
| 规则承载层级 | 常见项目只维护根规则 | 本项目按作用域拆到根级、目录级、包级多个 `AGENTS.md` | 新项目初始化时同步建立包级 `AGENTS.md` |
| 工件漂移 | 官方强调 specs/changes 一致 | 项目明确要求 design/specs/tasks 与代码同步，避免长期漂移 | 必须继承 |

## 什么属于“正常规则”

如果参考官方 OpenSpec 与大多数仓库的常见做法，“正常规则”通常有这些特征：

- 先初始化官方结构，再往里写项目上下文。
- 默认只区分 change 生命周期，不强制额外审批闸门。
- `apply` 完成后通常直接建议 archive，不一定强制单独 review 文档。
- 项目规范更多写在 `config.yaml` 和 `AGENTS.md`，而不是改动官方目录骨架。

## 什么属于“本项目高治理增强”

这些规则不是官方强制，但非常适合需要稳定协作的项目：

- 两道确认闸门，防止“分析完就直接写文档”或“文档一完就直接写代码”。
- coding 阶段显式接入 [Superpowers](https://github.com/obra/superpowers) 的实现、评审、验证技能，而不是只写成笼统的“开始 apply”。
- `apply -> 自动 review -> 等待确认 -> archive` 的连续治理链路。
- 归档前知识沉淀，要求把长期有效规则写回 `AGENTS.md`。
- 归档后默认继续收尾 Git 流程。
- 面向项目主入口、目录职责、外部框架封装的专项约束。
- 根规则之外，给每个包/目录维护独立 `AGENTS.md`，让规则在正确作用域落地。

## 迁移建议

- 想保持官方兼容性：用官方 `spec-driven`，不要把来源项目里的自定义 schema 当成所有项目的硬前提。
- 想保持项目一致性：把本项目的“治理增强”沉淀到模板和提示词，而不是改掉官方骨架。
- 想适配任意项目：只替换模板里的“技术栈、目录职责、主入口、领域边界、验证方式”，并按包结构生成对应 `AGENTS.md`。

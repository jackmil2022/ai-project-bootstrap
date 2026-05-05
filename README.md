# OpenSpec 项目初始化 Skill

这个仓库现在承载的是一个可复用的 skill：`openspec-project-bootstrap/`。

它的目标不是替代官方 OpenSpec，而是把“先保留官方结构，再叠加项目治理规则”的做法整理成一套可安装、可复用的技能资源，方便你在任意类型项目里复用。

## 这套包解决什么问题

- 先走官方初始化，不自造目录结构。
- 再把本项目沉淀出来的治理规则，补到 `openspec/config.yaml`、根 `AGENTS.md`、每个包级 `AGENTS.md`、以及项目级 OpenSpec 手册里。
- 把常用提示词按阶段分类，减少每次重新组织提示词的成本。

## 官方基线（以本机 `openspec 1.3.0` 实测为准）

建议先在目标项目里运行：

```bash
openspec init --tools codex
```

当前官方初始化默认会生成：

- `openspec/config.yaml`
- `openspec/changes/`
- `openspec/specs/`
- `openspec/changes/archive/`
- `.codex/skills/openspec-explore/`
- `.codex/skills/openspec-propose/`
- `.codex/skills/openspec-apply-change/`
- `.codex/skills/openspec-archive-change/`

这说明“官方方式”的核心，是保留官方目录和官方四阶段技能分类，而不是先发明一套自定义工作流。

## 这个 skill 怎么用

1. 使用 [`openspec-project-bootstrap/SKILL.md`](./openspec-project-bootstrap/SKILL.md) 作为技能入口。
2. 对照 `openspec-project-bootstrap/references/official-baseline-vs-project-rules.md`，判断要保留哪些官方基线、追加哪些治理规则。
3. 按 `openspec-project-bootstrap/references/bootstrap-any-project.md` 在目标项目落地。
4. 把 `openspec-project-bootstrap/assets/templates/` 下的模板拷入目标项目，再按项目实际情况替换占位符。
5. 按 `openspec-project-bootstrap/assets/prompts/` 下的分类提示词驱动后续 `explore / propose / apply / review / archive`。

## 目录说明

- `openspec-project-bootstrap/SKILL.md`：skill 入口与执行说明。
- `openspec-project-bootstrap/references/`：官方基线对照与初始化步骤。
- `openspec-project-bootstrap/assets/templates/`：可复制到目标项目的根级与包级模板。
- `openspec-project-bootstrap/assets/prompts/`：按阶段分类的提示词。
- `openspec-project-bootstrap/evals/evals.json`：最小测试提示词集合。

## 推荐原则

- 官方结构保持不变：继续使用官方 `openspec/` 目录和官方 `explore / propose / apply / archive` 分类。
- 初始化生成的目标项目里，项目补充规则分层承载：全局规则放根 `AGENTS.md`，包内规则放各包自己的 `AGENTS.md`，流程与上下文放 `openspec/config.yaml`、`openspec/CODEX_MANUAL.md`。
- 初始化生成的目标项目里，任何设计改动、行为改动或代码改动，都应先走 OpenSpec，再进入实现。
- `review` 作为项目治理补充阶段存在，不伪装成新的官方命令。
- `apply` 完成后自动进入 `review`，`review` 完成后停止并等待用户确认，再决定是否进入 `archive`。
- 初始化生成的目标项目里，coding / apply 阶段显式使用 `superpowers:test-driven-development`、`superpowers:requesting-code-review`、`superpowers:verification-before-completion`。
- 如果目标项目不需要中文，只需要把模板里的语言约束改掉，其余结构仍可复用。
- 包级目录默认都应有自己的 `AGENTS.md`，不要只靠根规则兜底。

## 推荐配套技能

- 如果目标环境支持插件或技能，建议安装 [Superpowers](https://github.com/obra/superpowers)。
- 在 OpenSpec 的 coding / apply 阶段，显式使用 `superpowers:test-driven-development`、`superpowers:requesting-code-review`、`superpowers:verification-before-completion`。

## 参考入口

- 官方 CLI 初始化说明：<https://openspec.clanker.guru/cli/init/>
- 官方 GitHub 仓库：<https://github.com/Fission-AI/OpenSpec>
- OpenSpec 规格格式说明：<https://thedocs.io/openspec/concepts/spec-format/>

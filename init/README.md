# OpenSpec 通用初始化包

这个目录的目标，不是替代官方 OpenSpec，而是把“本项目已经跑顺的规则”整理成一套可移植的初始化包，方便你在任意类型项目里复用，同时仍然坚持官方 OpenSpec 的落地方式。

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

## 本目录怎么用

1. 在目标项目里先执行官方初始化。
2. 对照 `01-官方基线与项目差异.md`，决定哪些规则要继承。
3. 按 `02-任意项目初始化步骤.md` 完成项目落地。
4. 把 `templates/` 下的模板拷入目标项目，再按项目实际情况替换占位符。
5. 按 `prompts/` 下的分类提示词驱动后续 `explore / propose / apply / review / archive`。

## 目录说明

- `01-官方基线与项目差异.md`：官方 OpenSpec 与本项目规则对照表。
- `02-任意项目初始化步骤.md`：任意项目的落地步骤。
- `templates/`：可复制到目标项目的根级与包级模板。
- `prompts/`：按阶段分类的提示词。

## 推荐原则

- 官方结构保持不变：继续使用官方 `openspec/` 目录和官方 `explore / propose / apply / archive` 分类。
- 项目补充规则分层承载：全局规则放根 `AGENTS.md`，包内规则放各包自己的 `AGENTS.md`，流程与上下文放 `openspec/config.yaml`、`openspec/CODEX_MANUAL.md`。
- `review` 作为项目治理补充阶段存在，不伪装成新的官方命令。
- `apply` 完成后自动进入 `review`，`review` 完成后停止并等待用户确认，再决定是否进入 `archive`。
- 如果目标项目不需要中文，只需要把模板里的语言约束改掉，其余结构仍可复用。
- 包级目录默认都应有自己的 `AGENTS.md`，不要只靠根规则兜底。

## 参考入口

- 官方 CLI 初始化说明：<https://openspec.clanker.guru/cli/init/>
- 官方 GitHub 仓库：<https://github.com/Fission-AI/OpenSpec>
- OpenSpec 规格格式说明：<https://thedocs.io/openspec/concepts/spec-format/>

# 补齐项目规则提示词

## 适用时机

- 官方初始化已经完成。
- 现在要把项目规则补齐到和本仓库类似的治理强度。

## 提示词

```text
请在不破坏官方 OpenSpec 结构的前提下，把当前项目补齐为“官方 OpenSpec + 项目治理增强”模式。

目标：
1. 保留官方 `openspec/` 目录和官方技能分类
2. 在 `openspec/config.yaml` 中补项目上下文与 per-artifact rules
3. 在根 `AGENTS.md` 中补全局长期规则
4. 为每个包级、领域级目录补自己的 `AGENTS.md`
5. 把 design / code change 必须先走 OpenSpec 的要求写清楚
6. 在 coding / apply 阶段显式接入 `superpowers:test-driven-development`、`superpowers:requesting-code-review`、`superpowers:verification-before-completion`
7. 如果项目需要严格流程，再新增 `openspec/CODEX_MANUAL.md`
8. 明确 `apply -> 自动 review -> 等待确认 -> archive` 的关系，但不要把 `review` 写成新的官方主命令

请重点梳理：
- 哪些改动必须走 OpenSpec
- 哪些设计改动或代码改动不能绕过 OpenSpec
- 是否需要第一确认闸门和第二确认闸门
- 主入口或主流程的兼容约束
- 目录职责
- 每个包级目录各自的局部规则
- 复用优先入口
- coding / apply 阶段显式使用哪些技能
- 测试与验证方式
- archive 前的知识沉淀要求

输出时请区分：
- 哪些属于官方基线
- 哪些属于项目补充规则
- 哪些应该写在根 `AGENTS.md`
- 哪些应该写在包级 `AGENTS.md`
```

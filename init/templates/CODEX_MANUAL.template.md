# OpenSpec 项目手册（模板）

本手册是项目级 OpenSpec 补充说明，用于在官方流程之上增加团队自己的治理规则。
默认前提是：根目录有全局 `AGENTS.md`，每个包级目录也有自己的 `AGENTS.md`。

## 1. 默认约定

- 默认输出语言：中文。
- 官方主流程保持为：`explore -> propose -> apply -> archive`。
- 如项目需要，可增加项目级 `review` 阶段：`apply -> 自动 review -> 等待确认 -> archive`。
- `openspec/changes/` 用于活跃变更，`openspec/changes/archive/` 仅保存历史。

## 2. 哪些场景必须走 OpenSpec

- 业务能力新增
- 功能变更
- 主流程调整
- 接口或数据结构变化
- 较大修复
- 会影响对外行为的改动

仅注释、说明文档、`AGENTS.md` 等不影响行为的少量文字调整，可按项目规则决定是否跳过。

## 3. 第一确认闸门

完成探索、代码调查、方案比较后，先向用户汇总：

- 当前理解
- 变更范围
- 候选方案 / 推荐方案
- 拟定 change 名称

只有在用户确认后，才创建或更新 proposal、design、specs、tasks。

## 4. 第二确认闸门

完成 OpenSpec 文档后，先向用户汇总：

- change 名称
- 关键假设
- 核心方案
- 任务拆分
- 主要风险

只有在用户确认后，才进入 apply 或任何实现动作。

## 5. review 阶段

如果项目采用高治理模式，则在 `apply` 完成后自动进入独立 review。

review 至少确认：

- 当前实现是否覆盖 proposal / specs / design / tasks
- 验证是否充分
- 是否存在行为回归或边界遗漏
- 当前 change 是否适合 archive

建议将结果记录到：

- `openspec/changes/<change-name>/review.md`

review 完成后，不得默认直接进入 archive，必须先向用户汇总结论并等待确认。

## 6. archive 前知识沉淀

archive 前回顾本次需求，提炼并沉淀：

- 实现边界
- 目录职责
- 复用入口
- 易错点
- 验证方式

长期有效规则放进最合适层级的 `AGENTS.md` 或项目文档，不记录一次性背景。
如果规则只影响某个包、模块或目录，优先沉淀到对应包级 `AGENTS.md`，不要一律回写根目录。

## 7. 维护要求

- 根 `AGENTS.md` 更新后，本手册需同步。
- OpenSpec schema、prompt、技能分类更新后，本手册也需同步。
- 多处描述冲突时，以更严格的约束为准。

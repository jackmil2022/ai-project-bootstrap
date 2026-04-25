# 创建提案提示词

## 适用时机

- 探索已经基本完成。
- 现在要正式创建 OpenSpec change 和 artifacts。

## 提示词

```text
请使用官方 OpenSpec 的 propose 方式，为当前需求创建 change，并生成进入实现前所需的工件。

执行要求：
1. 先确认 change 名称；如果没有明确名称，请基于需求生成 kebab-case 名称
2. 使用官方 OpenSpec CLI 创建 change
3. 按 schema 的依赖顺序生成 proposal、specs、design、tasks
4. proposal 重点写 why / what / impact
5. specs 重点写 requirement / scenario 的行为变化
6. design 只在跨模块、主流程、外部依赖、迁移、安全、性能等场景补充
7. tasks 要能直接驱动 apply

如果项目启用了严格治理，请在工件生成完成后停在“第二确认闸门”：
- 汇总 change 名称
- 汇总关键假设
- 汇总核心方案
- 汇总任务拆分
- 汇总主要风险

在我确认前，不要进入 apply，不要写测试，不要修改实现代码。
```

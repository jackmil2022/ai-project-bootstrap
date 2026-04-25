# 执行 Apply 提示词

## 适用时机

- proposal / specs / design / tasks 已准备好。
- 现在要开始实现，或继续推进未完成的 tasks。

## 提示词

```text
请使用官方 OpenSpec 的 apply 方式推进当前 change 的实现。

执行要求：
1. 先确认要使用的 change 名称
2. 读取 `openspec status --change "<name>" --json` 和 `openspec instructions apply --change "<name>" --json`
3. 读取 apply 阶段要求的上下文文件
4. 按 tasks 顺序实现，保持改动最小且聚焦
5. 每完成一项任务就同步更新 tasks 勾选状态
6. 实现完成后自动进入项目级 review
7. review 完成后，输出 review 结论并停止等待我确认是否进入 archive
8. 如果遇到设计分歧、需求不清、阻塞或风险扩大，立即暂停并说明

如果项目启用了第二确认闸门，请先确认我已经授权进入 apply。

额外要求：
- 不要跳过上下文文件直接写代码
- 不要把 apply 完成直接视为整个 change 完成
- 实现完成后，请自动进入项目级 review
- review 完成后，请停止并等待用户确认，而不是直接 archive
```

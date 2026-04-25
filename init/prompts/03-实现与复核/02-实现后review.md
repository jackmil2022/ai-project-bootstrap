# 实现后 Review 提示词

## 适用时机

- `apply` 已完成，或本轮实现与验证已完成。
- 现在要做独立复核，并在复核完成后停下来等待用户确认是否 archive。

## 提示词

```text
请基于当前 change 的 proposal、specs、design、tasks、实现代码和验证结果，执行一次独立 review。

重点检查：
1. 当前实现是否真正覆盖了 proposal / specs / design / tasks
2. 验证是否充分，是否缺关键场景
3. 是否存在行为回归、边界遗漏、实现偏差或残余风险
4. 当前 change 是否适合进入 archive

输出要求：
- 明确 review 范围
- 列出已完成验证
- 给出 findings / risks
- 给出结论：`passed` 或 `changes_requested`
- 明确是否允许进入 archive
- 明确当前状态为“等待用户确认”或“回到 apply”

如果项目有 `review.md` 约定，请把结论落到 `openspec/changes/<change-name>/review.md`。
如果发现问题，请回到 apply，而不是直接归档。
如果 review 通过，也不要直接归档，而是先停止等待用户确认。
```

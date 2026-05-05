# 归档与沉淀提示词

## 适用时机

- change 已完成实现。
- review 已通过，且用户已确认可以 archive；或项目允许带风险归档并已获得明确确认。

## 提示词

```text
请使用官方 OpenSpec 的 archive 方式归档当前 change，并在归档前完成项目知识沉淀。

执行要求：
1. 先确认要归档的 change 名称
2. 检查 artifacts、tasks、review 状态
3. 如果有 delta specs，先评估是否要同步到主 specs
4. 归档前提炼本次 change 的长期有效结论：
   - 实现边界
   - 目录职责
   - 复用入口
   - 易错点
   - 验证方式
5. 把长期有效规则写到最合适层级的 `AGENTS.md` 或项目文档；如果规则只影响某个包，优先写到该包的 `AGENTS.md`
6. 再执行 archive

补充要求：
- 不要机械地只改最近一级 `AGENTS.md`
- 不要把一次性任务背景写进长期规则
- 如果项目约定“archive 后继续 Git 收尾”，请在归档后继续检查工作区、说明提交范围，并协助执行 git add / commit / push
```

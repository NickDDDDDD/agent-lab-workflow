# Proposal

## Why

当前任务队列只能表达执行中、待派发和已完成，无法区分“尚未开始”和“因外部条件无法继续”。这会让开发者误判当前 Change 的真实进度，因此需要一个端到端可见的阻塞状态。

## What Changes

- 为任务状态展示增加 `blocked` 状态，并提供明确的“已阻塞”文本与独立视觉语气。
- 让共享设计组件、任务队列组件和前端示例数据使用同一项可观察状态语义。
- 保持现有 `active`、`waiting`、`idle` 和 `done` 行为不变。
- 不修改后端接口、持久化模型或依赖版本。

## Capabilities

### New Capabilities

- `task-status-presentation`: 定义任务状态在共享设计组件、任务队列和前端示例中的一致展示行为。

### Modified Capabilities

无。

## Impact

- `web-design`：扩展公共状态语气类型与 `StatusBadge` 的阻塞态样式。
- `web-plugin`：扩展任务状态契约并显示“已阻塞”标签。
- `web-front`：增加一个阻塞任务示例，证明消费链路可以构建。
- 公共类型联合会增加一个向后兼容的成员；现有调用方无需迁移。

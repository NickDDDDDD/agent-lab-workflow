# Proposal

## Why

`web-design` 的 README 目前只列出组件和样式，没有明确说明 Agent 运行时编排不属于该包。开发者可能因 Agent 相关页面语境而误把组件包当成运行时职责所有者，因此需要把已经由源码导出和消费者关系证明的边界写成可审查契约。

## What Changes

- 在 `web-design` README 中增加职责边界，明确该包只提供可复用视觉组件、公共类型与编译样式。
- 明确 Agent 生命周期、任务调度、网络请求和持久化不属于 `web-design`。
- 保持现有导出、依赖和运行时行为不变。

## Capabilities

### New Capabilities

- `web-design-package-boundary`: 规定组件包对开发者公开的职责与明确排除的运行时职责。

### Modified Capabilities

无。

## Impact

- 受影响仓库：`web-design`。
- 受影响文件：README 与本 Change 的 OpenSpec 规格。
- 不改变 JavaScript/CSS 输出、公共 API、依赖或消费者行为。

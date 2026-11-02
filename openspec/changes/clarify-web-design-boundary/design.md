# Design

## Context

见 `proposal.md` 的 Why。源码当前只导出 `LabButton`、`StatusBadge`、`StatusTone` 和样式；`web-plugin`、`web-front` 仅把它作为视觉依赖消费。现有 README 没有把这些事实归纳为明确的所有权边界。

## Goals / Non-Goals

**Goals:**

- 用一段靠近“使用边界”的 README 文本声明组件包职责。
- 让声明与当前源码导出和消费者关系一致。

**Non-Goals:**

- 不修改组件实现、公共导出、样式、依赖或构建产物。
- 不为运行时编排选择新的所有者或设计新的 Agent API。

## Decisions

### Decision: 在 README 中声明单一职责边界

把职责说明放在仓库公开 README，而不是新增 implementation notes 或独立架构文档。README 是使用者进入包的第一入口，且本次决定只描述现有公开边界，不构成需要长期独立治理的架构记录。

备选方案是只更新 OpenWiki；该方案不能保证首次查看包的开发者看到边界，因此不采用。

### Decision: 用现有导出和消费者构建作为验证

文档内容以源码导出和两类消费者的实际 import 为事实基础。实现只修改 README，验证运行 `npm run typecheck` 和 `npm run build`，不为纯文本新增伪造的代码测试。

## Risks / Trade-offs

- [边界说明未来可能随包职责变化而过时] → 规格和 README 同时进入评审，后续职责变更必须更新对应 requirement。
- [纯文档验证不能证明语义被所有人正确理解] → 使用明确的包含/排除列表，避免抽象口号。


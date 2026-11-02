# Design

## Context

`web-design/src/index.ts` 当前只导出 `LabButton`、`StatusBadge` 和 `StatusTone`，`package.json` 另行公开编译后的 `style.css`。`web-front` 与 `web-plugin` 仅通过公开包入口消费这些视觉能力。现有 README 没有把这些事实归纳为明确的所有权边界。

## Goals / Non-Goals

**Goals:**

- 用一段靠近“使用边界”的 README 文本声明组件包职责。
- 让声明与当前源码导出、包入口和消费者关系一致。

**Non-Goals:**

- 不修改组件实现、公共导出、样式、依赖或构建产物。
- 不为运行时编排选择新的所有者，也不设计新的 Agent API。

## Decisions

### Decision: 在 README 中声明单一职责边界

把职责说明放在仓库公开 README，而不是新增 implementation notes、ADR 或独立架构文档。README 是使用者进入包的第一入口，本次决定只描述现有公开边界，不形成第二套文档权威。

备选方案是只更新 OpenWiki。OpenWiki 是生成的按需证据索引，不能保证首次查看包的开发者看到边界，因此不采用。

### Decision: 用现有导出和消费者构建验证边界

文档内容以源码导出、包入口和消费者的实际 import 为事实基础。实现只修改 README；验证运行 `npm run typecheck` 与 `npm run build`，不为纯文本变更新增不能证明语义的伪代码测试。

## Risks / Trade-offs

- [边界说明未来可能随包职责变化而过时] → 规格和 README 同时进入评审，后续职责变更必须更新对应 requirement。
- [纯文档验证不能证明所有读者理解一致] → 使用明确的包含和排除列表，避免抽象口号。

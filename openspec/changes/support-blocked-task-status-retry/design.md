# Design

## Context

参见 `proposal.md` 的 Why。当前 `web-design` 通过 `StatusTone` 和 `StatusBadge` 维护共享视觉语气；`web-plugin` 维护任务领域类型与中文标签；`web-front` 提供消费端示例数据。三处类型边界都需要承认 `blocked`，否则 TypeScript 构建会在仓库边界暴露不一致。

## Goals / Non-Goals

**Goals:**

- 以最小的联合类型与映射扩展贯通三个前端仓库。
- 让可见文本承担状态语义，颜色只作为辅助提示。
- 使用现有类型检查和构建命令验证仓库边界。

**Non-Goals:**

- 不定义任务为何进入或离开阻塞状态。
- 不修改后端 API、调度逻辑或持久化。
- 不引入新的测试框架、样式依赖或跨仓发布机制。

## Decisions

### 1. 扩展现有状态联合而非建立第二套状态模型

在 `web-design` 的 `StatusTone` 中加入 `blocked`，并在 `web-plugin` 的 `Task.status` 中加入相同字面量。这样现有 `StatusBadge` 仍是唯一视觉组件，TypeScript 会在遗漏映射时给出穷尽性错误。

替代方案是给任务组件增加布尔型 `isBlocked`，但它会允许 `done + isBlocked` 等矛盾组合，因此不采用。

### 2. 使用文本标签与暖红色视觉语气共同表达阻塞

`TaskQueue` 显示固定标签“已阻塞”，`StatusBadge` 提供与现有四种语气不同的阻塞态样式。文本提供可访问的语义，颜色只增强扫描效率。

替代方案是复用 `waiting` 的黄色样式，但这无法帮助开发者区分等待调度与真实阻塞，因此不采用。

### 3. 用前端 fixture 证明跨仓消费契约

`web-front` 增加一个 `blocked` 任务样例；结合 `web-design` 和 `web-plugin` 的类型检查/构建命令，形成轻量的跨仓契约验证，不为本次验收引入额外测试框架。

### 4. 保持三个包 seam 的 Interface 单向收敛

`web-design` 的 `StatusTone` 是视觉语气 Module 的 Interface，隐藏具体样式实现；`web-plugin` 的 `Task.status` 是任务展示 Module 的 Interface，只把合法任务状态映射到视觉语气；`web-front` fixture 作为真实消费者跨越这两个 seam。实现顺序从设计系统到插件再到应用，避免调用方各自复制阻塞态样式或字符串。

替代方案是在 `web-front` 直接判断 `blocked` 并传入临时 class，但这会形成浅层透传并把视觉知识泄露到消费端，因此不采用。

## Risks / Trade-offs

- [Risk] 三个仓库分别维护字面量联合，未来可能再次漂移 → 依靠 TypeScript 消费链路和跨仓构建同时验证。
- [Risk] 阻塞态颜色在不同主题下对比度不足 → 保留明确文本标签，并选择与当前浅色徽标体系一致的高对比前景色。

## Migration Plan

1. 先扩展 `web-design` 的公共语气 Interface，使下游可引用阻塞态。
2. 再扩展 `web-plugin` 的任务 Interface 与文本映射。
3. 最后在 `web-front` fixture 中消费新状态并执行跨仓构建。

任一步失败都可以回退该仓对应提交；本次没有数据迁移、依赖升级或后端部署顺序。

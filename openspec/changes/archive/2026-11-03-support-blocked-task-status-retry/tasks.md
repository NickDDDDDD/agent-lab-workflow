# Tasks

## 1. 共享阻塞态语气

- [x] 1.1 在 `web-design` 的 `StatusTone` 与 `StatusBadge` 中加入 `blocked` 语气，并运行 `npm run typecheck` 与 `npm run build` 验证公共类型和样式映射
  **Blocked by:** None
  **Acceptance:** `blocked` 是合法公共语气且具有独立样式；原有四种语气保持可用；两个验证命令退出 0
  **Requirements:** task-status-presentation / 任务可以表达阻塞状态; task-status-presentation / 现有状态保持兼容

## 2. 任务队列阻塞语义

- [x] 2.1 在 `web-plugin` 的任务状态契约与标签映射中加入 `blocked`，并运行 `npm run typecheck` 与 `npm run build` 验证任务队列显示“已阻塞”
  **Blocked by:** 1.1
  **Acceptance:** `Task.status` 接受 `blocked`；队列映射为“已阻塞”；现有状态标签保持不变；两个验证命令退出 0
  **Requirements:** task-status-presentation / 任务可以表达阻塞状态; task-status-presentation / 阻塞状态可被明确识别; task-status-presentation / 现有状态保持兼容

## 3. 跨仓消费证明

- [x] 3.1 在 `web-front` fixture 中加入一个 `blocked` 任务样例，并运行 `npm run build` 验证设计组件、插件组件与消费端的跨仓状态契约
  **Blocked by:** 2.1
  **Acceptance:** fixture 包含阻塞任务；消费端能够使用 `blocked` 状态完成构建；不修改后端或增加依赖
  **Requirements:** task-status-presentation / 任务可以表达阻塞状态; task-status-presentation / 阻塞状态可被明确识别

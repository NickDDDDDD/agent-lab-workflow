# Tasks

## 1. 澄清组件包职责

- [ ] 1.1 在 `web-design` README 的使用边界中写明拥有的视觉组件、公共类型和样式职责，并明确排除 Agent 生命周期、任务调度、网络请求和持久化
  **Acceptance:** README 包含全部拥有和排除职责；`git diff` 仅涉及文档；没有修改组件源码、公共导出或依赖
  **Requirements:** web-design-package-boundary / README 声明组件包职责
- [ ] 1.2 保持现有公共导出不变并运行 `npm run typecheck` 与 `npm run build`
  **Acceptance:** 两个命令均退出 0；消费者源码零修改；现有 `LabButton`、`StatusBadge` 与 `StatusTone` 导出保持不变
  **Requirements:** web-design-package-boundary / 边界说明不改变包接口


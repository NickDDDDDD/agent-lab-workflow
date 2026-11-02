# Tasks

## 1. 澄清组件包职责

- [ ] 1.1 在 `web-design` README 的使用边界中写明本包拥有可复用视觉组件、公共类型和编译样式，并明确排除 Agent 生命周期、任务调度、网络请求和持久化；运行 `git diff --check`、`npm run typecheck` 与 `npm run build` 验证交付
  **Acceptance:** README 包含全部拥有和排除职责；业务仓差异仅涉及 README；三个验证命令均退出 0；消费者源码零修改；现有 `LabButton`、`StatusBadge`、`StatusTone` 与样式子路径保持不变
  **Requirements:** web-design-package-boundary / README 声明组件包职责; web-design-package-boundary / 边界说明不改变包接口

# Spec Delta

## Purpose

为 `web-design` 的使用者提供稳定、可验证的包职责说明，使视觉组件职责不会与 Agent 运行时、调度或数据职责混淆。

## ADDED Requirements

### Requirement: README 声明组件包职责

`web-design` 的公开 README SHALL 说明该包拥有可复用视觉组件、公共类型与编译样式，并 SHALL 明确 Agent 生命周期、任务调度、网络请求和持久化不属于该包。

#### Scenario: 开发者判断职责所有者

- **WHEN** 开发者阅读 `web-design` README 以确定某项 Agent 运行时能力应由哪个仓库实现
- **THEN** README 明确把该包限定为视觉组件、类型与样式提供者
- **AND** README 明确排除 Agent 生命周期、任务调度、网络请求和持久化职责

### Requirement: 边界说明不改变包接口

边界澄清 MUST 保持现有组件、类型、样式导出和消费者构建行为不变。

#### Scenario: 文档变更完成后验证包

- **WHEN** 边界说明写入 README 后执行类型检查与构建
- **THEN** `web-design` 现有公共导出继续通过验证
- **AND** 不需要修改消费者源码

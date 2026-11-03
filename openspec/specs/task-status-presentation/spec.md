# task-status-presentation Specification

## Purpose
定义任务阻塞状态在共享组件和消费端之间的一致、可辨识且可验证的展示契约，避免开发者把阻塞任务误认为普通等待任务。

## Requirements

### Requirement: 任务可以表达阻塞状态

任务展示链路 SHALL 接受 `blocked` 作为合法状态，并在设计组件、任务队列与前端示例之间保持该状态不丢失。

#### Scenario: 阻塞状态通过消费链路

- **WHEN** 前端向任务队列提供状态为 `blocked` 的任务
- **THEN** 任务队列和共享状态组件 SHALL 接受该值且项目构建成功

### Requirement: 阻塞状态可被明确识别

任务队列 SHALL 为阻塞任务显示“已阻塞”文本，并使用区别于执行中、待派发和已完成的视觉语气；状态含义不得仅依赖颜色表达。

#### Scenario: 开发者查看阻塞任务

- **WHEN** 任务队列渲染状态为 `blocked` 的任务
- **THEN** 界面 SHALL 显示“已阻塞”文本及对应的阻塞态徽标样式

### Requirement: 现有状态保持兼容

增加阻塞状态后，现有 `active`、`waiting`、`idle` 和 `done` 状态的公共类型与展示映射 MUST 保持可用。

#### Scenario: 现有状态继续构建

- **WHEN** 现有调用方继续使用原有状态值
- **THEN** 共享组件和任务队列 SHALL 继续通过类型检查与构建

---
created: 2025-09-05T00:47:32Z
last_updated: 2025-09-05T00:47:32Z
version: 1.0
author: Claude Code PM System
---

# System Patterns

## Architectural Design Patterns

### 1. Command Pattern Implementation
- **接口定义**: Markdown文件描述命令行为
- **实现分离**: Shell脚本提供具体功能
- **调度系统**: Claude Code解析Markdown并执行脚本
- **参数传递**: 通过环境变量和命令行参数

### 2. Agent Delegation Pattern
- **专用代理**: 每种任务类型有专门的AI代理
- **上下文优化**: 代理处理重任务，返回摘要
- **并行执行**: 多个代理同时工作在不同任务上
- **状态管理**: 代理间通过文件系统共享状态

### 3. GitHub-as-Database Pattern
- **Issues作为记录**: 每个任务成为GitHub Issue
- **Labels作为状态**: 使用标签管理工作流状态
- **Comments作为日志**: 进度更新记录在Issue评论中
- **API集成**: 通过GitHub CLI进行所有操作

### 4. Spec-Driven Development Pattern
- **PRD First**: 从产品需求文档开始
- **Epic Breakdown**: PRD转换为技术Epic
- **Task Decomposition**: Epic分解为可执行任务
- **Issue Tracking**: 任务同步到GitHub Issues

## Data Flow Architecture

### 1. 命令执行流
```
Markdown命令定义 → Claude Code解析 → Shell脚本执行 → 结果返回
```

### 2. 工作流状态流
```
PRD → Epic → Tasks → GitHub Issues → Parallel Agents → Code
```

### 3. 上下文流
```
项目分析 → 上下文文件 → 持久化存储 → 代理访问 → 状态更新
```

## Design Decisions

### 1. Markdown-Based Commands
- **原因**: 人类可读的接口定义
- **优势**: 易于文档化和维护
- **权衡**: 需要解析层，但提供了灵活性

### 2. File-Based Context
- **原因**: 持久化状态管理
- **优势**: 跨会话保持上下文
- **权衡**: 磁盘I/O，但避免了复杂的数据库依赖

### 3. Shell Script Implementation
- **原因**: Unix环境原生支持
- **优势**: 系统集成和工具链访问
- **权衡**: 平台依赖性，但提供了强大的系统控制

### 4. GitHub Issues Integration
- **原因**: 团队协作和透明度
- **优势**: 现有团队工具集成
- **权衡**: 依赖外部服务，但提供了协作价值

## Error Handling Patterns
- **Graceful Degradation**: 服务不可用时提供基本功能
- **Fail Fast**: 关键配置错误时快速失败
- **User Guidance**: 错误消息提供具体的修复建议
- **State Recovery**: 支持从中断状态恢复工作
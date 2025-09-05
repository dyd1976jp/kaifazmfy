---
created: 2025-09-05T00:47:32Z
last_updated: 2025-09-05T00:47:32Z
version: 1.0
author: Claude Code PM System
---

# Project Overview

## 系统功能概览

Claude Code Project Management (CCPM) 提供了一套完整的开发工作流管理功能，从需求规划到代码交付的全流程自动化。

## 主要特性列表

### 1. 项目管理命令 (`/pm:*`)
- **PRD管理**: 创建、编辑、解析产品需求文档
- **Epic管理**: 技术计划创建和状态跟踪
- **Issue管理**: GitHub Issues集成和状态同步
- **状态报告**: 项目进展和阻塞问题分析

### 2. 上下文管理 (`/context:*`)
- **上下文创建**: 自动生成项目上下文文档
- **上下文更新**: 保持项目状态同步
- **上下文加载**: 在新会话中快速恢复工作状态

### 3. 测试管理 (`/testing:*`)
- **测试环境配置**: 设置测试框架和工具
- **测试执行**: 自动化测试运行和结果分析

### 4. 代理系统
- **file-analyzer**: 文件内容分析和摘要
- **code-analyzer**: 代码分析和bug检测
- **test-runner**: 测试执行和结果分析
- **parallel-worker**: 并行任务执行协调

## 当前系统状态

### 已完成功能
- ✅ **命令系统**: 43个可用命令
- ✅ **脚本后端**: 完整的Shell脚本实现
- ✅ **GitHub集成**: Issues API完全集成
- ✅ **代理系统**: 4个专用代理可用
- ✅ **文档系统**: 完整的用户指南和技术文档
- ✅ **安装系统**: 跨平台安装脚本

### 核心工作流
1. **需求到规格**: `/pm:prd-new` → `/pm:prd-parse`
2. **规格到任务**: `/pm:epic-decompose` → `/pm:epic-sync`
3. **任务到代码**: `/pm:issue-start` → 并行代理执行
4. **进度跟踪**: `/pm:status` → `/pm:standup`

## 集成点

### GitHub Integration
- **Repository**: 必需的GitHub仓库
- **Issues**: 作为任务数据库
- **Labels**: 状态和优先级管理
- **Comments**: 进度更新和协作

### Claude Code Integration
- **Commands**: 通过.claude/commands/定义
- **Scripts**: Shell脚本执行后端
- **Agents**: 专用AI代理调用
- **Context**: 持久化状态管理

### Git Integration
- **Worktrees**: 并行开发环境隔离
- **Branches**: 功能分支管理
- **Commits**: 自动化提交和标记

## 部署架构

### 本地部署
- **要求**: Unix/Linux/macOS环境
- **依赖**: Claude Code CLI, Git, GitHub CLI
- **安装**: 单一脚本安装

### 远程协作
- **GitHub**: 中央协作平台
- **Issues**: 分布式任务管理
- **API**: 实时状态同步

## 性能特性
- **并行执行**: 多任务同时处理
- **上下文优化**: 智能信息摘要
- **增量更新**: 只同步变更内容
- **缓存机制**: 减少重复API调用
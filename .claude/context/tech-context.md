---
created: 2025-09-05T00:47:32Z
last_updated: 2025-09-05T00:47:32Z
version: 1.0
author: Claude Code PM System
---

# Technology Context

## Primary Technologies
- **Core Language**: Bash Shell Scripting
- **Command Interface**: Markdown-based definitions
- **Integration Platform**: GitHub Issues API
- **Deployment**: Unix/Linux/macOS native, Windows compatible

## Development Dependencies
- **Shell Environment**: Bash 3.0+ (macOS/Linux), PowerShell (Windows)
- **Git**: Version control and repository integration
- **GitHub CLI**: `gh` command for GitHub API interaction
- **Claude Code**: Anthropic's Claude Code CLI tool
- **System Tools**: Standard Unix tools (curl, grep, awk, sed)

## Framework Architecture
- **Command System**: Custom Markdown-to-Shell dispatch system
- **Agent Framework**: Sub-agent delegation for context optimization
- **GitHub Integration**: Native Issues API for project management
- **Context Management**: File-based persistent storage

## External Dependencies
### Required
- Claude Code CLI (主要运行时)
- GitHub CLI (`gh`) - 用于API交互
- Git - 用于版本控制和工作树管理
- Bash/Shell环境

### Optional
- Internet connection (GitHub API访问)
- GitHub repository (用于Issues集成)

## Language Versions
- **Bash**: 3.0+ (兼容macOS默认shell)
- **Git**: 2.0+ (支持worktree功能)
- **GitHub CLI**: 2.0+ (支持现代API功能)

## Architecture Patterns
- **Command Pattern**: Markdown定义 + Shell实现
- **Agent Pattern**: 专用子代理处理特定任务
- **State Management**: 基于文件的持久化上下文
- **API Integration**: GitHub Issues作为项目数据库

## Development Tools
- **Editor**: 任何支持Markdown和Shell脚本的编辑器
- **Testing**: 内置测试命令系统
- **Debugging**: Shell脚本调试和日志记录
- **Documentation**: 集成Markdown文档系统
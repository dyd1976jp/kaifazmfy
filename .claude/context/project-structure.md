---
created: 2025-09-05T00:47:32Z
last_updated: 2025-09-05T00:47:32Z
version: 1.0
author: Claude Code PM System
---

# Project Structure

## Root Directory Layout
```
kaifazmfy/
├── .claude/                    # Claude Code PM系统核心目录
│   ├── agents/                 # 专用代理定义
│   ├── commands/               # 命令定义 (Markdown格式)
│   │   ├── context/           # 上下文管理命令
│   │   ├── pm/                # 项目管理命令 (核心)
│   │   └── testing/           # 测试命令
│   ├── scripts/               # Shell脚本实现
│   │   └── pm/               # 项目管理脚本
│   ├── rules/                 # 行为规则和模式
│   └── context/              # 项目上下文存储 (本目录)
├── install/                   # 安装脚本和说明
├── README.md                  # 主要项目文档
├── COMMANDS.md               # 命令参考文档
├── AGENTS.md                 # 代理系统文档
├── LICENSE                   # MIT许可证
└── screenshot.webp          # 系统截图
```

## Key Directories

### `.claude/commands/` - 命令定义系统
- **格式**: Markdown文件定义命令接口
- **模式**: 每个命令一个.md文件
- **分类**: context/, pm/, testing/子目录

### `.claude/scripts/` - 脚本实现
- **语言**: Bash shell脚本
- **组织**: 与commands/目录结构对应
- **执行**: 通过Claude Code调用

### `.claude/context/` - 上下文管理
- **用途**: 存储项目状态和上下文信息
- **格式**: 结构化Markdown文件
- **版本控制**: 包含frontmatter元数据

## File Naming Patterns
- **命令定义**: `kebab-case.md` (例: `epic-decompose.md`)
- **脚本文件**: `kebab-case.sh` (与命令文件对应)
- **上下文文件**: `kebab-case.md` (描述性命名)

## Module Organization
- **命令系统**: 分离接口定义和实现
- **代理系统**: 独立的专用AI代理
- **文档系统**: 集中的项目说明和指南
- **安装系统**: 独立的部署脚本
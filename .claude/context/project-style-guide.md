---
created: 2025-09-05T00:47:32Z
last_updated: 2025-09-05T00:47:32Z
version: 1.0
author: Claude Code PM System
---

# Project Style Guide

## 编码标准和约定

### 命名约定

#### 文件命名
- **命令文件**: `kebab-case.md` (例: `epic-decompose.md`)
- **脚本文件**: `kebab-case.sh` (例: `epic-decompose.sh`)
- **上下文文件**: `kebab-case.md` (例: `project-structure.md`)
- **文档文件**: `kebab-case.md` 或 `UPPERCASE.md`

#### 变量命名 (Shell脚本)
- **环境变量**: `UPPER_SNAKE_CASE` (例: `GITHUB_TOKEN`)
- **本地变量**: `lower_snake_case` (例: `issue_number`)
- **函数名**: `lower_snake_case` (例: `create_epic`)

#### 命令命名
- **格式**: `/namespace:action-target`
- **示例**: `/pm:epic-decompose`, `/context:create`
- **原则**: 动词-名词结构，清晰描述功能

### 文件结构模式

#### Markdown命令定义结构
```markdown
# Command Title

Brief description of what this command does.

## Required Rules
[Any prerequisite rules or requirements]

## Instructions
[Detailed step-by-step instructions]

## Commands
[System commands to execute]

$ARGUMENTS
```

#### Shell脚本结构
```bash
#!/bin/bash
# Script description and purpose

# Set strict error handling
set -euo pipefail

# Function definitions
function main() {
    # Main logic here
}

# Execute main function
main "$@"
```

#### 上下文文件结构
```markdown
---
created: YYYY-MM-DDTHH:MM:SSZ
last_updated: YYYY-MM-DDTHH:MM:SSZ
version: X.Y
author: Claude Code PM System
---

# File Title

[Content organized with clear sections and subsections]
```

### 注释风格

#### Shell脚本注释
```bash
# Single line explanatory comment
function complex_operation() {
    # Explain why this approach was chosen
    local result
    result=$(some_command)
    
    # Handle edge cases
    if [[ -z "$result" ]]; then
        echo "Warning: No result from command" >&2
    fi
}
```

#### Markdown文档注释
```markdown
<!-- Internal note about implementation details -->
```

### 代码组织原则

#### 目录结构原则
- **分离关注点**: 命令定义与实现分离
- **模块化**: 按功能域组织 (pm/, context/, testing/)
- **可发现性**: 清晰的命名和目录结构
- **可维护性**: 相关文件放在相近位置

#### 文件组织原则
- **单一职责**: 每个文件专注一个功能
- **依赖最小化**: 减少文件间的紧耦合
- **接口标准化**: 统一的参数和返回值格式
- **错误处理**: 一致的错误处理和用户反馈

### 编程风格约定

#### Shell脚本风格
- **引号使用**: 变量总是用双引号包围 `"$variable"`
- **错误处理**: 使用 `set -euo pipefail`
- **函数定义**: 使用 `function name() { }` 格式
- **条件测试**: 使用 `[[ ]]` 而不是 `[ ]`

#### Markdown风格
- **标题层级**: 清晰的层级结构 (H1 > H2 > H3)
- **代码块**: 指定语言类型的代码块
- **列表格式**: 一致的列表符号和缩进
- **链接格式**: 使用相对路径引用内部文档

### 文档约定

#### 用户文档
- **语言**: 中文为主，技术术语保持英文
- **风格**: 直接、简洁、可操作
- **格式**: 使用标准Markdown格式
- **示例**: 提供具体的使用示例

#### 技术文档
- **完整性**: 包含所有必要的技术细节
- **准确性**: 与实际实现保持同步
- **可读性**: 清晰的结构和解释
- **维护性**: 包含更新日期和版本信息

### 版本控制约定

#### 提交消息格式
```
type(scope): description

- feat: 新功能
- fix: 错误修复
- docs: 文档更新
- refactor: 代码重构
```

#### 分支命名
- **功能分支**: `feature/description`
- **修复分支**: `fix/issue-number`
- **发布分支**: `release/version-number`

### 质量标准

#### 代码质量
- **可读性**: 代码即文档，清晰的命名和结构
- **健壮性**: 完善的错误处理和边界条件检查
- **可测试性**: 支持自动化测试的设计
- **可维护性**: 模块化设计，低耦合高内聚
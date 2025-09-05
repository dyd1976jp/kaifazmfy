---
name: video-subtitle-translate
status: backlog
created: 2025-09-05T06:30:32Z
progress: 0%
prd: .claude/prds/video-subtitle-translate.md
github: [Will be updated when synced to GitHub]
---

# Epic: video-subtitle-translate

## Overview

构建一个Python命令行工具，从MP4视频中提取音频，使用Whisper进行语音识别生成字幕，然后通过本地LLM（Ollama或LM Studio）进行翻译，最终输出标准双语SRT字幕文件。系统采用管道式架构，支持中断恢复，提供可选的交互式校对功能。

## Architecture Decisions

### 核心技术栈选择
- **Python 3.8+**: 丰富的音视频和ML生态系统
- **Whisper**: OpenAI开源语音识别模型，支持多语言高精度识别
- **Ollama/LM Studio**: 本地LLM运行时，支持多种开源模型（Qwen、Llama等）
- **FFmpeg**: 行业标准音视频处理工具
- **Click**: Python命令行界面框架

### 设计模式
- **Pipeline Pattern**: 音频提取 → 语音识别 → 翻译 → 格式化的流水线处理
- **Strategy Pattern**: 支持多种LLM模型和翻译策略
- **Template Method Pattern**: 统一的字幕处理模板，支持不同语言对
- **Observer Pattern**: 进度监控和日志记录

### 数据流设计
```
MP4输入 → AudioExtractor → WhisperSTT → LocalLLMTranslator → SRTFormatter → 双语SRT输出
            ↓               ↓              ↓                ↓
         临时音频文件    原始SRT文件    翻译缓存文件      最终输出文件
```

## Technical Approach

### 核心组件架构

#### 1. Audio Processing Module
- **FFmpeg包装器**: 提取MP4音频流为WAV格式
- **音频优化**: 降噪、标准化采样率为16kHz
- **分段处理**: 支持大文件分片处理，避免内存溢出
- **格式检测**: 自动检测音频编码格式和参数

#### 2. Speech Recognition Module
- **Whisper集成**: 使用whisper-python库进行本地识别
- **模型选择**: 支持tiny/base/small/medium/large模型选择
- **语言检测**: 自动检测音频语言或手动指定
- **时间轴生成**: 精确的单词级时间戳

#### 3. Translation Engine
- **多后端支持**: 支持Ollama和LM Studio两种本地LLM运行时
- **统一API接口**: 抽象层统一处理不同后端的API差异
- **自动检测**: 自动检测可用的LLM服务并选择最优后端
- **Prompt Engineering**: 优化翻译提示词，确保质量和格式
- **批处理优化**: 批量翻译减少API调用次数
- **错误重试**: 网络异常和模型错误的自动重试机制

#### 4. Subtitle Processing
- **SRT解析器**: 解析和生成标准SRT格式文件
- **双语格式化**: 上下行布局，翻译在上，原文在下
- **长度优化**: 根据语言特性调整字符数限制
- **时间轴校准**: 保持原始时间轴精度

#### 5. Interactive Review System (可选)
- **命令行界面**: 基于rich库的交互式TUI界面
- **逐句校对**: 显示原文、译文、时间轴信息
- **实时编辑**: 支持在线修改翻译内容
- **快捷键操作**: 接受/跳过/编辑的键盘快捷键

### 性能优化策略

#### 内存管理
- **流式处理**: 避免将整个音频文件加载到内存
- **LRU缓存**: 翻译结果缓存，避免重复翻译
- **垃圾回收**: 及时释放临时文件和内存对象

#### 并发处理
- **异步I/O**: 使用asyncio处理文件I/O和网络请求
- **进程池**: Whisper推理使用独立进程避免GIL限制
- **批处理**: 翻译请求批量处理，提高吞吐量

## Implementation Strategy

### 开发阶段划分

#### 阶段1: 核心管道 (3-4周)
1. 项目结构和配置管理
2. 音频提取和Whisper集成
3. 基本SRT文件生成和解析
4. 简单的LLM翻译集成

#### 阶段2: 翻译优化 (2-3周)
5. 翻译质量优化和prompt工程
6. 双语字幕格式化
7. 错误处理和重试机制

#### 阶段3: 用户体验 (2-3周)
8. 交互式校对界面
9. 命令行界面优化
10. 文档和测试完善

### 风险缓解
- **模型依赖**: 支持多个Whisper模型大小选择，平衡速度和精度
- **LLM质量**: 实现多种prompt策略和后处理规则
- **性能问题**: 分片处理和进度监控，支持中断恢复
- **兼容性**: 广泛的依赖版本测试和Docker容器化部署

### 测试策略
- **单元测试**: 每个组件的独立测试，覆盖率>90%
- **集成测试**: 端到端管道测试，使用多种视频样本
- **性能测试**: 大文件处理和内存使用测试
- **用户测试**: 真实场景下的可用性测试

## Tasks Created

- [ ] 001.md - 项目搭建和配置 (parallel: false, depends_on: [])
- [ ] 002.md - 音频处理模块 (parallel: true, depends_on: [001])
- [ ] 003.md - Whisper语音识别 (parallel: true, depends_on: [001])
- [ ] 004.md - 本地LLM翻译 (parallel: true, depends_on: [001])
- [ ] 005.md - 双语字幕生成 (parallel: false, depends_on: [003, 004])
- [ ] 006.md - 交互式校对界面 (parallel: true, depends_on: [005])
- [ ] 007.md - 命令行界面 (parallel: false, depends_on: [002, 003, 004, 005])
- [ ] 008.md - 测试和文档 (parallel: false, depends_on: [001-007])

**总计任务**: 8
**并行任务**: 4 (002, 003, 004, 006)
**串行任务**: 4 (001, 005, 007, 008)
**预估总工作量**: 18-22天

### 任务依赖关系
```
001 (项目搭建) 
├── 002 (音频处理) ─┐
├── 003 (Whisper) ─┼─→ 005 (双语字幕) ─┐
└── 004 (LLM翻译) ─┘                 ├─→ 007 (CLI界面) ─┐
    006 (校对界面) ←─────────────────┘                ├─→ 008 (测试文档)
                                                      ┘
```

## Dependencies

### 外部服务依赖
- **本地LLM服务**: Ollama或LM Studio，需要预先安装和配置（二选一）
  - Ollama: 命令行友好，自动模型管理
  - LM Studio: GUI界面，用户友好，手动模型管理
- **FFmpeg**: 系统级音视频处理工具，跨平台安装
- **Python包生态**: whisper、click、rich、requests等核心依赖

### 模型依赖
- **Whisper模型**: 需要下载对应大小的模型文件（160MB-3GB）
- **LLM模型**: Qwen2.5、Llama3等多语言翻译模型（4GB-32GB）

### 系统依赖
- **硬件要求**: 现代CPU（AVX支持），最少16GB内存，50GB存储空间
- **操作系统**: macOS 10.15+、Ubuntu 18.04+、Windows 10+

### 关键路径
1. **Whisper模型验证** → **本地LLM环境测试（Ollama/LM Studio）** → **核心管道开发** → **质量优化**
2. **多后端兼容性测试**和**性能基准测试**是验收的关键依赖

## Success Criteria (Technical)

### 性能基准
- **处理速度**: 30分钟视频在10分钟内完成（3倍速）
- **内存使用**: 峰值内存占用 < 8GB
- **准确率**: Whisper识别准确率 > 90%，翻译BLEU > 0.4
- **时间精度**: 字幕时间轴误差 < 0.5秒

### 质量指标
- **格式合规**: 100%符合SRT标准格式
- **字符限制**: 严格遵守字符数限制（中25/英50/日25）
- **编码支持**: 支持UTF-8和常见特殊字符
- **错误处理**: 优雅处理90%+的常见错误场景

### 可用性指标
- **CLI友好性**: 直观的命令行参数和帮助信息
- **错误提示**: 清晰的错误信息和解决建议
- **进度反馈**: 实时处理进度和预估完成时间
- **文档完整性**: 安装、使用、故障排除完整文档

## Estimated Effort

### 总体时间线
- **开发周期**: 8-10周（符合PRD要求的8-12周范围）
- **核心开发**: 6-7周
- **测试优化**: 1-2周
- **文档发布**: 1周

### 资源需求
- **开发人员**: 1名全栈Python开发者
- **专业技能**: 音视频处理、NLP、Python生态系统熟悉
- **硬件资源**: 开发机器需要支持本地LLM运行

### 关键里程碑
1. **Week 4**: 核心管道MVP完成，可处理简单视频
2. **Week 6**: 翻译质量达标，支持三语言对
3. **Week 8**: 交互界面完成，用户体验优化
4. **Week 10**: 测试完成，文档发布准备

### 风险预留
- 预留20%时间buffer处理模型集成和性能优化问题
- 翻译质量调优可能需要额外1-2周时间
- 跨平台兼容性测试可能发现意外问题
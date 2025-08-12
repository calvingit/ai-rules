# AI 规则 - Flutter 开发规范与最佳实践

专为 Flutter 开发者设计的 AI 工具提示词和开发规范集合。本项目旨在通过经过验证的最佳实践，标准化 AI 辅助开发工作流并确保代码质量。

## 🎯 项目目的

本仓库记录并整理了在使用 Cursor、WindSurf、Trae 等 AI 开发工具处理 Flutter 项目时的专业提示词、代码规范、设计指南和项目规则。通过建立统一标准，确保 AI 生成的代码遵循最佳实践，最小化回归风险，并提高可维护性。

## 📁 项目结构

```
ai-rules/
├── README.md                    # 项目文档（英文版）
├── README-zh.md                 # 项目文档（中文版）
├── flutter-agent-prompt.md      # 高阶AI Agent提示词（上下文工程版）
├── flutter-chat-complex-prompt.md # 复杂问题专家级提示词
├── flutter-chat-prompt-simple.md # 简单问题基础提示词
├── flutter-code-rules.md        # Flutter/Dart代码规范与最佳实践
├── flutter-design-guidelines.md # Flutter应用设计指南
├── flutter-project-rule.md      # Flutter项目工程规范
└── CLAUDE.md                    # Claude专用配置
```

## 📋 文件说明

### 1. flutter-agent-prompt.md - 高阶 AI Agent 配置

专为具备上下文工程能力的复杂 AI Agent 设计：

- **角色定义**：资深 Flutter 工程师 AI 助手
- **工作流程**：6 步标准化开发流程
- **工具策略**：外部化大内容、循环驱动开发
- **编码准则**：最小侵入性改动、可回滚方案
- **架构原则**：分层设计、依赖倒置、单一职责
- **输出模板**：标准化交付格式

### 2. flutter-chat-complex-prompt.md - 复杂问题专家提示词

针对复杂技术挑战的专家级指导：

- **知识领域**：涵盖 Dart 语言特性、状态管理、性能优化等 12 个专业领域
- **诊断能力**：问题根本原因分析与解决方案策略
- **架构建议**：项目架构设计和技术选型指导
- **原理说明**：深入技术原理和权衡考量解释

### 3. flutter-chat-prompt-simple.md - 基础提示词配置

简洁的 Flutter AI 助手配置，适用于：

- 日常开发任务
- 快速代码生成
- 基础问题解答

### 4. flutter-code-rules.md - 全面代码规范

完整的 Flutter/Dart 代码规范，包括：

- **命名规范**：类、函数、变量和文件的命名标准
- **类型系统**：类型注解和泛型使用指南
- **代码风格**：格式化和结构最佳实践
- **文档标准**：注释格式和 API 文档要求
- **测试指南**：单元测试和组件测试原则

### 5. flutter-design-guidelines.md - 设计指南

全面的 Flutter 应用开发指南，定义：

- **技术栈**：Flutter SDK 版本、第三方库选择标准
- **目录结构**：模块化项目结构示例
- **架构模式**：Clean Architecture、分层架构实现
- **开发标准**：从项目初始化到部署的完整工作流

### 6. flutter-project-rule.md - 工程规范

项目级工程规范，确保：

- **版本管理**：Flutter/Dart SDK 版本控制
- **模块职责**：各层级的清晰职责边界
- **依赖管理**：第三方库选择和版本控制标准
- **性能优化**：内存管理和渲染性能最佳实践

## 🚀 使用指南

### 基于场景的选择

| 场景          | 推荐文件                                               | 使用方法                 |
| ------------- | ------------------------------------------------------ | ------------------------ |
| 新项目初始化  | flutter-design-guidelines.md + flutter-project-rule.md | 作为项目初始规范         |
| 日常开发辅助  | flutter-chat-prompt-simple.md                          | 配置为 AI 工具基础提示词 |
| 复杂问题解决  | flutter-chat-complex-prompt.md                         | 针对具体技术问题咨询     |
| 代码审查      | flutter-code-rules.md                                  | 作为代码审查标准         |
| AI Agent 开发 | flutter-agent-prompt.md                                | 配置到自动化 AI Agent    |

### AI 工具集成

#### Cursor 配置

Cursor 支持两种规则配置方式，根据使用场景选择合适的方式：

**方式一：项目特定配置（推荐）**
创建`.cursor/rules`目录并在其中添加规则文件：

```bash
# 创建规则目录
mkdir -p .cursor/rules

# 对于Flutter项目
cp flutter-chat-prompt-simple.md .cursor/rules/flutter.mdc

# 对于复杂项目
cp flutter-agent-prompt.md .cursor/rules/agent.mdc
```

**方式二：全局配置**
在 Cursor 设置中配置全局规则：
1. 打开 Cursor Settings (⌘/Ctrl + ,)
2. 进入 General > Rules for AI
3. 粘贴对应的提示词内容

**优先级说明**：项目特定的`.cursor/rules/`目录规则优先级高于全局Rules for AI设置。

**注意**：`.cursorrules`文件方式已废弃，请使用新的`.cursor/rules/`目录结构。

#### Trae 配置

在 Trae 项目设置中，将提示词添加到项目规则中。

#### 其他 AI 工具

根据各工具支持的方式进行配置。

## 🎯 核心优势

1. **专业性强**：所有规则基于 Flutter 官方最佳实践和实际项目经验
2. **层次分明**：从基础到高级，满足不同复杂度项目需求
3. **实战导向**：每个规范都配有实际应用场景和代码示例
4. **持续更新**：根据 Flutter 生态发展持续优化
5. **可定制性**：可根据具体项目需求灵活调整

## 📈 最佳实践建议

### 新项目启动流程

1. 阅读`flutter-design-guidelines.md`了解整体架构
2. 根据`flutter-project-rule.md`设置项目规范
3. 配置 AI 工具使用合适的提示词
4. 开发过程中参考`flutter-code-rules.md`确保代码质量

### 现有项目优化

1. 使用`flutter-code-rules.md`进行代码审查
2. 针对具体问题使用`flutter-chat-complex-prompt.md`获取专业建议
3. 逐步引入规范，避免大范围重构

## 🤝 贡献指南

欢迎社区贡献和反馈：

- 提交 Issue 讨论规范改进
- 分享实际项目中的最佳实践
- 提出新的规范建议

## 📄 许可证

本项目采用 MIT 许可证，可自由使用和修改。

## 🌏 国际化

- [English Version](README.md)
- [中文版](README-zh.md)

## 📞 联系与支持

如有问题或建议，欢迎通过以下方式联系：

- 提交 GitHub Issue
- 参与讨论和改进
- 分享您的使用经验
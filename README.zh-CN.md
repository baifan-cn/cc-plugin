# TokenRoll Claude Code 插件

<div align="center">

**通过 sub-agent 架构解决 Claude Code 的上下文爆炸问题**

节省 83% 上下文 | 研究驱动开发 | 智能工作流

[![GitHub](https://img.shields.io/badge/GitHub-TokenRollAI%2Fcc--plugin-blue?logo=github)](https://github.com/TokenRollAI/cc-plugin)

[English](README.md) | [简体中文](README.zh-CN.md)

</div>

---

## 关于

由 **DJJ** 和 **Danniel** 为 TokenRoll 团队开发的强大 Claude Code 插件。本插件通过智能 Git 自动化、研究优先开发模式和创意构思工具，彻底改变你的开发工作流。

## ✨ 核心特性

### 🤖 智能 Git 工作流
**`/tr:commit`** - 从你的 Git 历史中学习的智能提交信息生成器
- 分析你的提交风格（emoji 使用、conventional commits、语言习惯）
- 生成描述"为什么"而非"是什么"的上下文化提交信息
- 自动遵循你团队的现有规范

### 🔍 上下文高效研究（核心创新）
**`/tr:withScout`** + **Scout Agent** - **通过 sub-agent 架构节省 83% 上下文**

**问题所在：**
Claude Code 在中大型项目上因全量文件读取导致上下文爆炸。
- 传统方式：**83K 上下文** → 容易触及限制 ❌

**解决方案：**
Sub-agent 执行大量读取 → 提供精简总结 → 主 agent 保持清爽
- withScout 方式：**29K 上下文** → 相同质量，节省 83% token ✅

**核心优势：**
- 🎯 **节省 83% 上下文** - 实际使用中验证（29K vs 83K tokens）
- 🔒 Sub-agent 独立上下文隔离
- 📚 大量读取操作不污染主上下文
- ⚡ 支持多领域并行研究
- 💎 只输出结构化的高价值信息

**适用场景：** 中大型项目的重构、bug修复、功能规划、文档编写

*基于：* [Claude Code Sub-agents](https://docs.claude.com/en/docs/claude-code/sub-agents) | [社区讨论](https://linux.do/t/topic/1031049)

### 💡 病毒式产品创意
**Super-Idea Agent** - 将热门话题转化为病毒式产品概念
- 分析病毒传播机制和情感触发点
- 设计针对分享优化的 AI 驱动产品概念
- 优先考虑新颖性和爆发式增长潜力
- 适用于头脑风暴会议和创新冲刺

---

## 🚀 快速开始

### 安装

在 Claude Code 中运行以下命令：

```bash
# 添加 TokenRoll 插件市场
/plugin marketplace add TokenRollAI/cc-plugin

# 安装插件
/plugin install tr@cc-plugin
```

安装完成后，**重启 Claude Code** 以激活插件。

### 基本用法

```bash
# 生成智能提交信息
/tr:commit

# 研究优先工作流：先理解再实现
/tr:withScout 我想重构认证系统

# 病毒式创意构思，直接在对话中调用 super-idea agent
```

---

## 🧠 withScout 如何解决上下文爆炸问题

### Claude Code 的上下文问题

Claude Code 在小型项目上表现出色，但在中大型代码库上会遇到一个根本性问题：**全量文件读取导致的上下文爆炸**。

**传统工作流：**
1. 用户提问："项目中的 Operator 有什么作用？数据存储和流转是怎么实现的？"
2. Claude 读取 50+ 个文件来理解代码库
3. 所有文件内容加载到对话上下文中
4. **结果：消耗 83K tokens**（不包括 17K 初始上下文）
5. 快速接近上下文限制，需要重启对话

[参考 Linux.do 上的讨论 →](https://linux.do/t/topic/1031049)

### Sub-Agent 解决方案

**withScout 利用 Claude Code 的 sub-agent 架构来隔离重度操作：**

```
┌─────────────────────────────────────────────────────┐
│  主 Agent（你的对话）                                │
│  上下文：干净聚焦                                    │
│  ✅ 只接收结构化总结                                 │
└─────────────────────────────────────────────────────┘
              ↓ 委托研究任务
┌─────────────────────────────────────────────────────┐
│  Scout Sub-Agent（隔离的上下文）                     │
│  • 读取代码库中的 50+ 个文件                         │
│  • Grep 模式匹配和符号搜索                           │
│  • 执行网络搜索获取文档                              │
│  • 将发现总结为精简报告                              │
│  上下文：重度操作在这里隔离 ⚡                       │
└─────────────────────────────────────────────────────┘
              ↓ 只返回总结
┌─────────────────────────────────────────────────────┐
│  主 Agent 接收：                                     │
│  ✅ 【Research Summary】 - 关键发现                  │
│  ✅ 【Recommendations】 - 可行的后续步骤             │
│  ❌ 不是：50 个完整文件内容倾倒在上下文中            │
└─────────────────────────────────────────────────────┘
```

**核心原理：** Sub-agent 拥有独立上下文，不会污染主对话。非常适合「大量读取 → 总结」的工作流。

### 实际效果

**测试案例：** *"项目中的 Operator 有什么作用？数据存储和流转是怎么实现的？"*

| 方式 | 主 Agent 上下文 | 上下文明细 | 节省比例 |
|------|----------------|-----------|---------|
| **不使用 sub-agent** | 83K tokens | 初始：17K + 研究：**70K** | - |
| **使用 `/tr:withScout`** | 29K tokens | 初始：17K + 总结：**12K** | **83%** |

**计算方式：**
- 传统方式为主 agent 增加 **70K 上下文**（全量文件读取）
- withScout 仅为主 agent 增加 **12K 上下文**（结构化总结）
- **节省：58K tokens = 83% 减少**

### 为什么这很重要

✅ **处理更大的项目** - 能够处理通常会导致上下文爆炸的代码库
✅ **更长的对话** - 持续工作而不触及 token 限制
✅ **并行研究** - 启动多个 scout 而不污染上下文
✅ **更清爽的体验** - 主 agent 专注于你的实际任务
✅ **成本效率** - 使用更少 token 的同时保持质量

### 实现细节

- **Scout Agent：** 专业 sub-agent，配备 Read、Glob、Grep、WebSearch、WebFetch 工具（[源码](https://github.com/TokenRollAI/cc-plugin/blob/main/agents/scout.md)）
- **withScout 命令：** 工作流编排器，调用 scout 并处理结果（[源码](https://github.com/TokenRollAI/cc-plugin/blob/main/commands/withScout.md)）
- **架构基础：** 基于 [Claude Code 的 sub-agents](https://docs.claude.com/en/docs/claude-code/sub-agents)，提供独立上下文隔离

---

## 📖 功能详解

### 命令

#### `/tr:commit` - 智能提交信息生成器

具备风格感知能力的自动化提交工作流：

**功能说明：**
1. 并行收集 git 信息（diff、status、log）
2. 分析项目的提交历史以学习风格模式
3. 生成符合你的规范的提交信息
4. 提供提交、修改或重新生成选项

**示例工作流：**
```bash
/tr:commit

# 输出：
# 正在分析变更...
# - 发现 src/auth/ 中有 3 个文件被修改
# - 检测到使用 emoji 的 conventional commits 风格
# - 最近的提交使用 "feat:", "fix:", "refactor:" 前缀
#
# 建议的提交信息：
# ✨ feat: add JWT token refresh mechanism
#
# - Implement automatic token refresh before expiration
# - Add refresh token rotation for security
# - Handle edge cases for offline token refresh
#
# [提交] [修改] [重新生成]
```

**核心功能：**
- 从 git log 中学习 emoji 使用模式
- 检测 conventional commits、gitmoji 或自定义格式
- 遵守字符数限制（英文 50-72 字符）
- 描述动机和影响，而非仅仅列举变更

---

#### `/tr:withScout` - 研究优先工作流

先研究再实现的元工作流：

**模式：**
```
用户请求 → Scout 研究 → 实现 → 总结
```

**使用场景：**

```bash
# 场景 1：重构
/tr:withScout 我想重构用户认证系统
# → Scout 收集：当前认证实现、依赖关系、设计模式
# → 你收到：结构化发现 + 推荐方案
# → 然后：在充分了解的基础上实现

# 场景 2：修复 bug
/tr:withScout 修复 Redis 缓存失效问题
# → Scout 调查：缓存实现、Redis 配置、已知问题
# → 你收到：根因分析 + 修复建议
# → 然后：自信地应用修复方案

# 场景 3：编写文档
/tr:withScout 为支付接口创建 API 文档
# → Scout 收集：端点定义、请求/响应结构、认证要求
# → 你收到：全面的端点信息
# → 然后：生成准确的文档
```

**为什么使用它？**
- 自动化研究，节省时间
- 确保在编码前拥有完整上下文
- 减少试错迭代
- 支持复杂任务的并行研究

**上下文效率：**
- 🎯 **节省 83% 上下文** - 相比传统方式（29K vs 83K tokens）
- Scout 在隔离的 sub-agent 上下文中执行大量读取
- 主 agent 只接收高价值总结，而非原始文件倾倒
- 能够探索大型代码库而不触及上下文限制
- 完美适用于上下文管理至关重要的中大型项目

---

### Agent

#### `tr:scout` - 专业研究专家

从代码库和网络收集信息的专业 agent。

**可用工具：** Read, Glob, Grep, WebSearch, WebFetch

**核心能力：**
- 深度代码库分析（文件搜索、内容 grep、模式匹配）
- 网络研究获取文档、最佳实践和解决方案
- 上下文感知研究（提供已知上下文时避免重复工作）
- 并行研究支持（多个 scout 可同时工作）

**输出格式：**
```
【Research Summary】
研究发现的简要概述

【Key Findings】
• 关键发现 1
• 关键发现 2
• 关键发现 3

【Detailed Analysis】
深入调查结果...

【Recommendations】
可行的后续步骤...

【Sources】
检查的文件和 URL
```

**高级用法 - 并行侦察：**
```bash
# 为复杂研究启动多个 scout
# Scout 1：后端架构
# Scout 2：前端组件
# Scout 3：数据库模式
# Scout 4：API 集成
# Scout 5：最佳实践的网络研究
```

---

#### `tr:super-idea` - 病毒式产品创意生成器

将热门话题转化为爆炸性产品概念。

**可用工具：** Read, Write, Grep, Glob

**五步方法论：**
1. **解构趋势** - 识别情感触发点（幽默、愤怒、好奇、自豪）
2. **设计核心机制** - 创建简单、令人上瘾的交互（15 秒内吸引注意力）
3. **注入 AI 能力** - 利用 AIGC、AI 推荐或 AI 分析
4. **设计病毒传播触发器** - 设计爆炸性分享机制
5. **输出概念** - 结构化、可执行的格式

**输出格式：**
```
【Concept Name】
朗朗上口、令人难忘的产品名称

【One-Line Pitch】
"[产品] 是 [描述]，它能 [独特价值]"

【Core Mechanics】
• 用户如何交互（15 秒内吸引）
• 核心功能（3-5 个要点）

【AI Integration】
• AI 如何驱动体验
• 使用的具体 AI 能力

【Viral Trigger Analysis】
• 用户为什么会分享
• 心理钩子
• 网络效应
```

**设计哲学：**
- 病毒性优先，商业模式其次
- 拒绝已验证市场，追求新颖性
- 为爆炸性分享设计，而非稳定增长
- 适合头脑风暴，不适合生产规划

---

## 🛠️ 开发指南

### 项目结构

```
cc-plugin/
├── .claude-plugin/
│   ├── marketplace.json  # 市场清单
│   └── plugin.json       # 插件配置（id: "tr"）
├── commands/             # 自定义斜杠命令
│   ├── hello.md         # 演示命令
│   ├── commit.md        # Git 工作流自动化
│   └── withScout.md     # 研究驱动工作流
├── agents/               # 自定义 agent
│   ├── helper.md        # 通用助手
│   ├── scout.md         # 研究专家
│   └── super-idea.md    # 病毒式创意工具
└── hooks/                # 事件钩子
    └── hooks.json       # 钩子配置
```

### 添加新命令

在 `commands/` 目录下创建新的 `.md` 文件：

```markdown
---
description: 简短的命令描述
---

# 命令标题

Claude Code 执行此命令的详细说明。
包括分步工作流、预期输入和输出。
```

### 添加新 Agent

在 `agents/` 目录下创建新的 `.md` 文件：

```markdown
你是 [agent 名称]，一个 [角色描述]。

## 核心能力
- 能力 1
- 能力 2

## 工作流程
1. 步骤 1
2. 步骤 2

## 输出格式
指定预期的输出结构...
```

### 配置钩子

编辑 `hooks/hooks.json` 以添加在特定操作（工具调用、用户提示等）时触发的事件钩子。

---

## 📚 参考资源

- [Claude Code 文档](https://docs.claude.com/en/docs/claude-code)
- [插件开发指南](https://docs.claude.com/en/docs/claude-code/plugins)
- [插件市场](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)

---

## 📄 许可证

仅供内部使用 - TokenRoll 团队

---

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>

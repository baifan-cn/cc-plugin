# TokenRoll Claude Code 插件

<div align="center">

**TokenRoll 团队开发并使用的 Claude Code 插件**

[![GitHub](https://img.shields.io/badge/GitHub-TokenRollAI%2Fcc--plugin-blue?logo=github)](https://github.com/TokenRollAI/cc-plugin)

[English](README.md) | [简体中文](README.zh-CN.md)

</div>

---

## 关于

这是由 **DJJ** 和 **Danniel** 创建的 Claude Code 插件，TokenRoll 团队开发并使用。本插件提供了一系列自定义命令、代理和工作流，帮助团队成员更高效地使用 Claude Code 进行日常开发工作。

## 🚀 安装方法

### 方式 1: 从 GitHub 安装（推荐）

```bash
# 添加 TokenRoll 插件市场
/plugin marketplace add TokenRollAI/cc-plugin

# 安装插件
/plugin install tokenroll-std@cc-plugin

# 重启 Claude Code 以激活插件
```

### 方式 2: 本地安装

如果你已经克隆了仓库到本地：

```bash
# 导航到你的项目目录并启动 Claude Code
cd /path/to/your/project
claude

# 插件将从当前目录自动加载
```

## 📦 插件结构

```
cc-plugin/
├── .claude-plugin/
│   ├── marketplace.json  # 市场清单
│   └── plugin.json       # 插件清单
├── commands/             # 自定义斜杠命令
│   └── hello.md
├── agents/               # 自定义代理
│   └── helper.md
└── hooks/                # 事件钩子
    └── hooks.json
```

## 💡 可用命令

- `/hello` - 向用户发送个性化问候

## 🛠️ 开发指南

### 添加新命令

在 `commands/` 目录下创建新的 `.md` 文件：

```markdown
---
description: 命令描述
---

# 命令标题

命令的详细说明和行为。
```

### 添加新代理

在 `agents/` 目录下创建新的 `.md` 文件，定义代理的行为和专长。

### 配置钩子

编辑 `hooks/hooks.json` 来添加事件钩子。

## 📚 参考资源

- [Claude Code 插件官方文档](https://docs.claude.com/en/docs/claude-code/plugins)
- [插件市场官方文档](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)

## 📄 许可证

仅供内部使用 - TokenRoll 团队

---

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>

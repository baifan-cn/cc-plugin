# TokenRoll Claude Code Plugin

<div align="center">

**A custom Claude Code plugin developed and used by TokenRoll team**

[![GitHub](https://img.shields.io/badge/GitHub-TokenRollAI%2Fcc--plugin-blue?logo=github)](https://github.com/TokenRollAI/cc-plugin)

[English](README.md) | [简体中文](README.zh-CN.md)

</div>

---

## About

This is a custom Claude Code plugin developed and used by TokenRoll team, created by **DJJ** and **Danniel**. It provides a collection of custom commands, agents, and workflows to help team members work more efficiently with Claude Code.

## 🚀 Installation

### Method 1: Install from GitHub (Recommended)

```bash
# Add the TokenRoll plugin marketplace
/plugin marketplace add TokenRollAI/cc-plugin

# Install the plugin
/plugin install tokenroll-std@cc-plugin

# Restart Claude Code to activate the plugin
```

### Method 2: Local Installation

If you've cloned the repository locally:

```bash
# Navigate to your project directory and start Claude Code
cd /path/to/your/project
claude

# The plugin will be automatically loaded from the current directory
```

## 📦 Plugin Structure

```
cc-plugin/
├── .claude-plugin/
│   ├── marketplace.json  # Marketplace manifest
│   └── plugin.json       # Plugin manifest
├── commands/             # Custom slash commands
│   └── hello.md
├── agents/               # Custom agents
│   └── helper.md
└── hooks/                # Event hooks
    └── hooks.json
```

## 💡 Available Commands

- `/hello` - Greet the user with a personalized message

## 🛠️ Development Guide

### Adding New Commands

Create a new `.md` file in the `commands/` directory:

```markdown
---
description: Command description
---

# Command Title

Detailed description and behavior of the command.
```

### Adding New Agents

Create a new `.md` file in the `agents/` directory to define agent behavior and expertise.

### Configuring Hooks

Edit `hooks/hooks.json` to add event hooks.

## 📚 Resources

- [Claude Code Plugin Documentation](https://docs.claude.com/en/docs/claude-code/plugins)
- [Plugin Marketplaces Documentation](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)

## 📄 License

Internal use only - TokenRoll Team

---

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>

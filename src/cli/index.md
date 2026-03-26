---
title: "Elementor CLI"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Cli
    - Src
    - Repos
---

# Elementor CLI

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 集成了 [WP-CLI](https://wp-cli.org/)，使您能够通过命令行界面运行某些 Elementor 任务，而无需使用网页浏览器。

## 什么是 WordPress CLI？

WP-CLI 是 [WordPress](https://wordpress.org/) 的命令行界面。它提供了 WordPress 管理栏的替代方案。使用命令行使开发者、代理商和托管服务提供商能够更轻松地以更少的点击次数运行操作、远程运行它们，甚至可以根据特定条件执行复杂的脚本。

## 什么是 Elementor CLI？

Elementor CLI 是一组集成到 WP-CLI 中的命令，允许开发者从命令行运行某些 Elementor 任务。

## 语法

CLI 命令语法：

```bash
wp elementor <command> [--argument]
```

或

```bash
wp elementor-pro <command> [--argument]
```

## 可用命令

目前，以下 Elementor 命令可用：

* [系统信息](src/cli/system-info)
* [刷新 CSS](src/cli/flush-css)
* [替换 URL](src/cli/replace-urls)
* [更新数据库](src/cli/update-db)
* [库同步](src/cli/library-sync)
* [库连接](src/cli/library-connect)
* [库断开连接](src/cli/library-disconnect)
* [库导入](src/cli/library-import)
* [库导入目录](src/cli/library-import-dir)
* [清除主题生成器条件](src/cli/theme-builder-clear-conditions)
* [工具包导入](src/cli/kit-import)
* [工具包导出](src/cli/kit-export)
* [实验状态](src/cli/experiments-status)
* [实验激活](src/cli/experiments-activate)
* [实验停用](src/cli/experiments-deactivate)
* [许可证激活](src/cli/license-activate)
* [许可证停用](src/cli/license-deactivate)

## 帮助

要通过命令行查看所有可用 Elementor 命令的列表，请使用 `wp help` 命令。

要获取单个命令的信息，请使用以下格式：

```bash
wp help elementor <command>
```

或

```bash
wp help elementor-pro <command>
```
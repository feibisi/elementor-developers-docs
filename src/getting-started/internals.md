---
title: "Elementor 内部机制"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Getting Started
    - Src
    - Repos
---

# Elementor 内部机制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 拥有底层技术，我们称之为内部机制。在本节中，我们将介绍开发 Elementor 插件时需要理解的概念。

## 可用的内部机制

以下是 Elementor 内部机制的列表，附有简短说明和深入信息的链接：

* [编辑器](src/editor)

  编辑器是用户创建页面和控制设置的地方。它分为预览区和面板区。面板承载小部件列表，是用户控制设置的地方。预览屏幕是他们查看页面外观的地方。

* [管理器](src/managers)

  Elementor 的架构使用特殊的管理器来注册和注销元素。外部开发者需要使用这些管理器来注册自己的元素。这将让 Elementor 知道它们的存在，从而启用它们。

* [脚本与样式](src/scripts-styles)

  开发者需要了解不同的 Elementor 组件如何加载自定义 JS 和 CSS 文件。由于这些文件可能严重影响性能，学习为每个组件加载它们的正确方法非常重要。

* [钩子](src/hooks)

  Elementor 提供了广泛的钩子供使用。本文档包含了 Elementor 提供的所有可用钩子的完整列表——过滤器钩子、动作钩子、PHP 钩子、JS 钩子、前端钩子和编辑器钩子。

* [弃用功能](src/deprecations)

  随着时间的推移，代码会被移除或替换。弃用过程是渐进的，Elementor 的弃用过程包含几个步骤。开发者需要了解 Elementor 如何弃用代码，以及他们如何调试和更新已弃用的代码。

* [命令行界面](src/cli)

  Elementor 与 WP-CLI 集成，使开发者能够通过命令行界面运行某些 Elementor 任务，而无需使用 Web 浏览器。所有可用命令及其参数和使用示例都列在此处。

* [构建插件](src/addons)

  本节包含针对不熟悉 WordPress 的人员的信息。它讨论了基本的 WordPress 插件开发，以及 Elementor 插件和高级主题，包括插件和面向对象编程的背景信息。
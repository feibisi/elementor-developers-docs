---
title: "构建扩展插件"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Addons
    - Src
    - Repos
---

# 构建扩展插件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 扩展插件本质上是为 Elementor 增加功能的 WordPress 插件。在开始创建 Elementor 扩展插件之前，你需要具备创建 WordPress 插件的背景知识。之后，你需要学习 Elementor 扩展插件构建的基础知识。

## WordPress 插件

[WordPress](https://wordpress.org/) 拥有一个高度可扩展的代码库。它允许任何人通过使用插件来扩展核心功能。如需深入了解，请查阅 [WordPress 开发者资源](https://developer.wordpress.org/) 中的 [插件手册](https://developer.wordpress.org/plugins/)。

## Elementor 扩展插件

在创建 Elementor 扩展插件时，你应该遵循所有 WordPress 编码标准和最佳实践。此外，你还应遵循本网站概述的 Elementor 标准和最佳实践。

要开始创建 Elementor 扩展插件，你首先需要构建一个专注于 Elementor 的简单 WordPress 插件，请参考以下信息：

* [文件与文件夹结构](src/addons/file-folder-structure)
* [头部注释](src/addons/plugin-header)
* [加载过程](src/addons/load)
* [主类](src/addons/main-class)
* [兼容性检查](src/addons/compatibility)
* [初始化过程](src/addons/initialization)
* [使用命名空间](src/addons/namespaces)
* [扩展插件示例](src/addons/addon-example)

## 下一步是什么？

当你完成构建一个包装器后，就可以开始扩展 Elementor 组件了。请查看以下教程，了解如何扩展各个组件的详细信息和示例：

* [创建新小部件](src/widgets)
* [创建新控件](src/controls)
* [创建新动态标签](src/dynamic-tags)
* [创建新表单动作](src/form-actions)
* [创建新表单字段](src/form-fields)
* [创建新查找器类别](src/finder)
* [扩展上下文菜单](src/context-menu)

当然，这些只是扩展 Elementor 的一些方式。
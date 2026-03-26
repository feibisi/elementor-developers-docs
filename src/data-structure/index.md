---
title: "数据结构"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Data Structure
    - Src
    - Repos
---

# 数据结构

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 依赖特定的数据结构来运行。该结构在平台的流程中扮演着重要角色，对其操作至关重要。开发者应熟悉 Elementor 数据结构的关键方面，包括其格式和应用。

## Elementor 引擎

整个 Elementor 引擎由多个与 Elementor 数据层交互的组件组成。它是 Elementor 功能不可或缺的一部分，并贯穿其所有操作。

引擎功能有两个不同的方面：
- 编辑器负责通过可视化的拖放界面创建结构化数据。
- 前端负责解析页面数据以创建页面布局。

## 数据格式

在数据格式方面，Elementor 使用 JSON 来构建数据，因为它易于人类读写，也易于机器解析和生成。JSON 文件广泛用于以结构化方式交换数据，这使其成为 Elementor 的实用选择。

## 保存的数据

Elementor JSON 数据结构用于存储使用 Elementor 创建的页面的配置和内容。它是页面布局及其设置的序列化表示。

JSON 数据是标准化的，因此可以导出和导入，以便在不同的页面和不同的 WordPress 安装中复制页面设计。

## 数据存储

当用户在编辑器中点击保存按钮时，Elementor 将页面数据和布局以 JSON 格式存储为 WordPress 文章元数据，这本质上是一个 WordPress 自定义字段。WordPress 将自定义字段存储在数据库的 [wp_postmeta](https://codex.wordpress.org/Database_Description#Table:_wp_postmeta) 表中。

Elementor 数据被保存为私有自定义字段，在 WordPress 仪表板中不可见。访问数据的一个简单方法是下载 Elementor "模板" 文件。此操作会创建一个包含页面数据的 `*.json` 文件。

## Elementor 数据结构

要了解 JSON 文件的结构，请阅读以下内容：

* [通用结构](src/data-structure/general-structure)
* [页面设置](src/data-structure/page-settings)
* [页面内容](src/data-structure/page-content)

有关不同元素类型的信息：

* [通用元素](src/data-structure/general-elements)
* [容器元素](src/data-structure/container-element)
* [小部件元素](src/data-structure/widget-element)

特殊情况：

* [响应式数据](src/data-structure/responsive-data)
* [重复器](src/data-structure/repeaters)
* [全局样式](src/data-structure/global-styles)
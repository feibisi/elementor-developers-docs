---
title: "Finder 分类"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Finder
    - Src
    - Repos
---

# Finder 分类

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

查找器返回一组按分类组织的链接。每个分类包含指向网站不同部分的链接。对于用户输入的每个搜索词，查找器会根据相关的“关键词”过滤链接列表。

## 可用分类

默认情况下，查找器提供对以下链接组的快速访问：

*   **创建** (_`create`_) – 提供与创建新文章/页面/模板等相关的链接。
*   **编辑** (_`edit`_) – 提供与编辑文章/页面/模板等相关的链接。
*   **常规** (_`general`_) – 提供与 Elementor 相关的常规链接。
*   **设置** (_`settings`_) – 提供与 Elementor 设置相关的链接。
*   **工具** (_`tools`_) – 提供与 Elementor 工具相关的链接。
*   **站点** (_`site`_) – 提供与站点相关的链接。

## Finder 钩子

Finder 分类有两个开发者可以使用的钩子：

*   `elementor/finder/register` 动作 - 用于注册新的查找器分类。
*   `elementor/finder/categories` 过滤器 - 用于修改查找器分类数组。
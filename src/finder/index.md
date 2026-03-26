---
title: "Elementor Finder"
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

# Elementor Finder

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Finder 组件会打开一个弹出式搜索栏，方便快捷地访问网站上的许多页面和设置。它可用于创建新文章、编辑其他页面、导航到不同的设置页面等。

<img :src="$withBase('/assets/img/elementor-finder.png')" alt="Elementor Finder">

## Finder 结构

Finder 包含一个[类别](src/finder/finder-categories)数组。每个类别包含多个**项目**。每个项目都包含一个标签、一个链接和一组关键词。当用户输入搜索词时，Finder 会根据相关的关键词筛选项目列表。

了解更多关于 [finder 结构](src/finder/finder-structure)、其主类以及可用方法的信息。

## 扩展 Finder

外部开发者可以注册自己的自定义 Finder 类别及其自定义链接。了解更多：

* [添加新的 Finder 项目](src/finder/add-new-finder-items)
* [向现有类别添加项目](src/finder/add-items-to-existing-category)
* [移除 Finder 类别](src/finder/remove-finder-categories)
* [移除 Finder 项目](src/finder/remove-finder-items)

## 代码示例

看看扩展 Finder 是多么容易：

* [简单示例](src/finder/simple-example)
* [高级示例](src/finder/advanced-example)
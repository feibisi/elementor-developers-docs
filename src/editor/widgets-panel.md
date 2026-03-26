---
title: "小部件面板"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor
    - Src
    - Repos
---

# 小部件面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/widgets-panel.png')" alt="Elementor Widgets Panel" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

**小部件** 是 [编辑器](src/editor) 中的入口面板（用户看到的第一个面板）。用户可以从此处将小部件拖放到 [预览](src/editor/elementor-preview) 区域。

## 结构与功能

该面板有两个选项卡：

* **元素** - 已注册小部件的列表。
* **全局** - 用户保存的全局小部件列表。

元素选项卡按类别分组显示网站的小部件。它还有一个搜索栏，可用于筛选小部件。

全局选项卡显示所有已保存的小部件及其设置和设计。全局小部件可在多个区域和多个页面上使用。更改全局小部件会影响所有页面上该小部件的所有实例。

## 扩展小部件面板

Elementor 开箱即用提供了数十个小部件。尽管如此，外部开发者可以 [创建新的小部件](src/widgets)，甚至可以将它们组织到自己的品牌 [小部件类别](src/widgets/widget-categories) 中。
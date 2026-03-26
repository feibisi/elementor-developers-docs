---
title: "站点设置面板"
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

# 站点设置面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/site-settings-panel.png')" alt="Elementor Site Settings Panel" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

**站点设置**是[编辑器](src/editor)中的一个面板，用户可以在其中全局定义站点设置。这包括全局颜色、排版、站点标识等。

## 结构与功能

该面板包含三个部分：

*   **设计系统** - 定义全局颜色和字体，以确保设计一致性。
*   **主题样式** - 由主题处理的全局设计层。
*   **设置**

设计系统允许用户创建自定义配色方案和排版，以便在不同的部件中使用。它使用户能够创建统一的设计，并轻松更改整个站点的方案。

主题样式是常规的主题设置，为各种 HTML 元素创建预设的回退样式。如果未为特定部件设置定义，则使用主题样式。

设置部分允许您设置站点标识、布局、断点、自定义 CSS 等。
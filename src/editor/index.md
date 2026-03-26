---
title: "Elementor 编辑器"
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

# Elementor 编辑器

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

编辑器是用户创建页面和控制网站设置的环境。编辑器是一个通用术语，包含两个主要区域——预览区和面板区。每个区域都包含可由第三方开发者扩展的内部区域。

## 结构

编辑器指整个编辑屏幕，由两个主要区域组成：

* [Elementor 预览区](src/editor/elementor-preview)
* [Elementor 面板区](src/editor/elementor-panel)

## 编辑器面板

面板区域显示各种控件和设置。显示的控件和功能取决于当前显示的具体面板：

* [菜单面板](src/editor/menu-panel)
* [网站设置面板](src/editor/site-settings-panel)
* [用户偏好设置面板](src/editor/user-preferences-panel)
* [页面设置面板](src/editor/page-settings-panel)
* [历史记录面板](src/editor/history-panel)
* [小部件面板](src/editor/widgets-panel)
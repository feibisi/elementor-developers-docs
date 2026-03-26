---
title: "菜单面板"
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

# 菜单面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/menu-panel.png')" alt="Elementor Menu Panel" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

**菜单面板**是[编辑器](src/editor)中的主面板。用户可由此导航至其他面板。换言之，它充当着其他 Elementor 面板的仪表板。

## 结构与功能

该面板包含两个部分：

* **设置** - 链接至控制设置的其他面板。
* **页面导航** - 链接至外部链接和工具。

## 扩展菜单面板

开发者可以向菜单面板添加新链接。为保持一致性，这些链接应打开其他 Elementor 面板。
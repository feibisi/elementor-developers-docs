---
title: "Elementor 面板"
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

# Elementor 面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

面板就像一个编辑仪表盘。这是用户可以控制页面所有方面的区域。它包括全局设置、页面设置、小部件面板等。

<img :src="$withBase('/assets/img/elementor-panel.png')" alt="Elementor Panel">

## Elementor 面板

面板区域由多个面板组成：

* [菜单面板](src/editor/menu-panel)
* [站点设置面板](src/editor/site-settings-panel)
* [用户偏好设置面板](src/editor/user-preferences-panel)
* [页面设置面板](src/editor/page-settings-panel)
* [历史记录面板](src/editor/history-panel)
* [小部件面板](src/editor/widgets-panel)

## 扩展面板

其中一些面板是可扩展的。开发者可以向现有面板添加新元素，并且我们正在开发一种创建新面板的官方方法，以替代目前一些插件作者使用的变通方案。
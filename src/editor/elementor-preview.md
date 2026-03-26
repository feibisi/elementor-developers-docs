---
title: "Elementor 预览"
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

# Elementor 预览

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

预览区域用于显示当前正在编辑页面的实时预览。它由 JavaScript 引擎渲染，通常无需从服务器端加载。换句话说，这是您可以看到网站最终呈现效果的区域。

<img :src="$withBase('/assets/img/elementor-preview.png')" alt="Elementor Preview">

## 扩展预览功能

预览区域是编辑器的一部分。这意味着它继承了部分编辑功能，允许用户控制外观样式。开发者可以利用这些功能来扩展预览区域。例如：

* [内联编辑](src/widgets/rendering-inline-editing) - 开发 [Elementor 小部件](src/widgets) 时，可使元素在预览中直接编辑
* [上下文菜单](src/context-menu) - 在预览中右键点击元素时，可在上下文弹出窗口中添加操作链接
* **编辑按钮** - 在预览中悬停元素时，可添加新的编辑按钮
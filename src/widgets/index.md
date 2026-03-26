---
title: "Elementor 小工具"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Widgets
    - Src
    - Repos
---

# Elementor 小工具

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor 在**小工具面板**中内置了数十个实用的小工具。这些小工具按类别划分。每个小工具都有一套自定义控件（输入字段），允许最终用户输入数据。

<img :src="$withBase('/assets/img/elementor-widgets.png')" alt="Elementor Widgets Panel" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

## 管理小工具

外部开发者可以注册新的小工具或注销现有小工具。了解更多操作方法：

* [添加新小工具](src/widgets/add-new-widget)
* [移除小工具](src/widgets/remove-widgets)

## 创建新小工具

了解更多关于小工具的构成以及如何创建自己的小工具：

* [小工具结构](src/widgets/widget-structure)
* [小工具数据](src/widgets/widget-data)
  * [小工具信息](src/widgets/widget-information)
  * [小工具推广](src/widgets/widget-promotions)
  * [小工具类别](src/widgets/widget-categories)
* [小工具依赖项](src/widgets/widget-dependencies)
* [小工具控件](src/widgets/widget-controls)
* [小工具渲染](src/widgets/widget-rendering)
  * [小工具设置](src/widgets/widget-settings)
  * [渲染文本](src/widgets/rendering-text)
  * [渲染样式](src/widgets/rendering-style)
  * [渲染媒体](src/widgets/rendering-media)
  * [渲染重复器](src/widgets/rendering-repeaters)
  * [渲染 HTML 属性](src/widgets/rendering-html-attribute)
  * [渲染内联编辑](src/widgets/rendering-inline-editing)
  * [小工具输出缓存](src/widgets/widget-output-caching)

## 代码示例

查看创建 Elementor 小工具是多么简单：

* [简单示例](src/widgets/simple-example)
* [高级示例](src/widgets/advanced-example)
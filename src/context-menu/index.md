---
title: "Elementor 上下文菜单"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Context Menu
    - Src
    - Repos
---

# Elementor 上下文菜单

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

上下文菜单是一个弹出菜单，当用户在 [Elementor 预览](src/editor/elementor-preview) 区域右键单击某个元素时出现。此弹出菜单根据位置或所选元素提供一组可用的操作。这就是它被称为上下文菜单的原因。

<img :src="$withBase('/assets/img/elementor-context-menu.png')" alt="Elementor Context Menu">

## 上下文菜单结构

Elementor 根据所选元素或其位置有几种 [类型](src/context-menu/context-menu-types) 的上下文菜单。开发者可以挂钩到任何元素类型并修改其操作。

每个菜单分为几个 [组](src/context-menu/context-menu-groups)，每组包含多个项目。上下文菜单组通过分隔符在视觉上分开。

每个菜单项称为一个 [操作](src/context-menu/context-menu-actions)。操作是应用于所选元素（部分、列、小部件）的 JS 回调函数。

## 扩展上下文菜单

外部开发者可以注册自己的自定义操作并修改现有操作。

学习管理组：

* [添加新的上下文菜单组](src/context-menu/add-new-group)
* [移除上下文菜单组](src/context-menu/remove-group)
* [更新上下文菜单组](src/context-menu/update-group)

学习管理操作：

* [添加新的上下文菜单操作](src/context-menu/add-new-action)
* [移除上下文菜单操作](src/context-menu/remove-action)
* [更新上下文菜单操作](src/context-menu/update-action)

## 代码示例

查看这些示例以了解上下文菜单的实际创建：

* [简单示例](src/context-menu/simple-example)
* [高级示例](src/context-menu/advanced-example)
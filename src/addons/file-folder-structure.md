---
title: "文件与文件夹结构"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Addons
    - Src
    - Repos
---

# 文件与文件夹结构

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

所有 [WordPress 插件指南](https://developer.wordpress.org/plugins/plugin-basics/best-practices/#file-organization) 都应适用于 Elementor 插件。您应保持文件夹结构简单，并将相似的文件放在一起。

## 文件

您的插件根目录 `/elementor-test-addon/` 应包含一个 `elementor-test-addon.php` 文件。最佳实践是使文件夹和主文件同名。

``` {3}
elementor-test-addon/
|
└─ elementor-test-addon.php
```

其他文件是可选的。如果插件有其他文件，应尽可能将它们组织到子文件夹中。

## 文件夹

最佳实践是将相似的文件放在一起。例如，您应将 CSS 文件分组在一起，JS 文件分组在一起。此规则也适用于文件类型和功能——例如，“小部件”应分组在一起，控件应分组在一起等。

### 单一组件插件

创建单一组件插件时，可以使用更简单的文件夹结构：

```
elementor-test-addon/
|
├─ assets/
|
├─ widgets/
|
└─ elementor-test-addon.php
```

### 多组件插件

随着插件变得更大、更复杂，您应将文件组织到文件夹中。我们推荐以下文件夹结构：
```
elementor-test-addon/
|
├─ assets/
|  ├─ images/
|  ├─ css/
|  └─ js/
|
├─ includes/
|  ├─ controls/
|  ├─ dynamic-tags/
|  ├─ finder/
|  └─ widgets/
|
└─ elementor-test-addon.php
```
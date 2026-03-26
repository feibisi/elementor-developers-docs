---
title: "禁用 Google 字体加载"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Hooks
    - Src
    - Repos
---

# 禁用 Google 字体加载

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 提供了一个特殊的过滤器钩子，允许开发者阻止 Google 字体的加载。换句话说，并非所有前端 Google 字体都会被加入队列。

## 钩子详情

* **钩子类型：** 过滤器钩子
* **钩子名称：** `elementor/frontend/print_google_fonts`
* **影响范围：** 前端

## 控制 Google 字体入队

要阻止 Elementor 在前端加载 Google 字体：

```php
/**
 * 阻止 Elementor 在前端加载 Google 字体。
 *
 * @since 1.0.0
 */
add_filter( 'elementor/frontend/print_google_fonts', '__return_false' );
```
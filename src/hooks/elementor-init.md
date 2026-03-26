---
title: "Elementor 初始化"
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

# Elementor 初始化

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 提供了一个钩子，在插件完全加载时触发。

## 钩子详情

* **钩子类型:** 动作钩子
* **钩子名称:** `elementor/init`
* **影响范围:** 初始化过程

## 示例

```php
function my_plugin() {

	// ...

}
add_action( 'elementor/init', 'my_plugin' );
```
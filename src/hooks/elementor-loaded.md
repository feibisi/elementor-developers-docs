---
title: "Elementor 已加载"
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

# Elementor 已加载

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 有一个钩子，会在插件加载后、加载所有组件之前触发。

## 钩子详情

* **钩子类型:** 动作钩子
* **钩子名称:** `elementor/loaded`
* **影响范围:** 初始化过程

## 示例

```php
function my_plugin() {

	// ...

}
add_action( 'elementor/loaded', 'my_plugin' );
```
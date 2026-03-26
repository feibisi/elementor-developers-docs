---
title: "移除动态标签"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Dynamic Tags
    - Src
    - Repos
---

# 移除动态标签

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

要移除现有的动态标签，开发者只需通过传递动态标签名称来注销现有标签。

## 钩子

为此，我们需要挂载到包含动态标签管理器的 `elementor/dynamic_tags/register` 动作，并将动态标签名称传递给 `unregister()` 方法。

## 注销动态标签

要注销现有的动态标签，请使用以下代码：

```php
function unregister_dynamic_tags( $dynamic_tags_manager ) {

	$dynamic_tags_manager->unregister( 'dynamic-tag-1' );
	$dynamic_tags_manager->unregister( 'dynamic-tag-2' );

}
add_action( 'elementor/dynamic_tags/register', 'unregister_dynamic_tags' );
```
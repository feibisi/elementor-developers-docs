---
title: "添加新的动态标签"
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

# 添加新的动态标签

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 提供了许多开箱即用的内置动态标签，同时也允许外部开发者注册新的标签。

## 钩子

为此，我们只需挂载到 `elementor/dynamic_tags/register` 动作，该动作将动态标签管理器作为参数提供。开发者可以使用管理器的 `register()` 方法，通过动态标签实例来添加新标签。

## 注册动态标签

使用以下代码注册新的动态标签：

```php
function register_new_dynamic_tags( $dynamic_tags_manager ) {

	require_once( __DIR__ . '/dynamic-tags/dynamic-tag-1.php' );
	require_once( __DIR__ . '/dynamic-tags/dynamic-tag-2.php' );

	$dynamic_tags_manager->register( new \Elementor_Dynamic_Tag_1() );
	$dynamic_tags_manager->register( new \Elementor_Dynamic_Tag_2() );

}
add_action( 'elementor/dynamic_tags/register', 'register_new_dynamic_tags' );
```

管理器通过接受动态标签实例来注册新标签。有关动态标签类的更多信息，请阅读[动态标签类结构](src/dynamic-tags/dynamic-tags-structure)。
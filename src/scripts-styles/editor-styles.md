---
title: "编辑器样式"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Scripts Styles
    - Src
    - Repos
---

# 编辑器样式

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

当你开发扩展 [Elementor 编辑器](src/editor) 的插件并拥有自定义样式表时，请使用 `elementor/editor/before_enqueue_styles` 或 `elementor/editor/after_enqueue_scripts` 动作钩子，这些钩子会在编辑器样式注册和入队时触发。

## 注册编辑器样式

在下面的示例中，我们将在 Elementor 样式注册和入队**之前**注册并加入自定义样式表：

```php {6,12}
function my_plugin_register_editor_styles() {
	wp_register_style( 'editor-style-1', plugins_url( 'assets/css/editor-style-1.css', __FILE__ ) );
	wp_register_style( 'editor-style-2', plugins_url( 'assets/css/editor-style-2.css', __FILE__ ), [ 'external-framework' ] );
	wp_register_style( 'external-framework', plugins_url( 'assets/css/libs/external-framework.css', __FILE__ ) );
}
add_action( 'elementor/editor/before_register_styles', 'my_plugin_register_editor_styles' );

function my_plugin_enqueue_editor_styles() {
	wp_enqueue_style( 'editor-style-1' );
	wp_enqueue_style( 'editor-style-2' );
}
add_action( 'elementor/editor/before_enqueue_styles', 'my_plugin_enqueue_editor_styles' );
```

现在，我们将在 Elementor 样式注册和入队**之后**注册并加入自定义样式表：

```php  {6,12}
function my_plugin_register_editor_styles() {
	wp_register_style( 'editor-style-1', plugins_url( 'assets/css/editor-style-1.css', __FILE__ ) );
	wp_register_style( 'editor-style-2', plugins_url( 'assets/css/editor-style-2.css', __FILE__ ), [ 'external-framework' ] );
	wp_register_style( 'external-framework', plugins_url( 'assets/css/libs/external-framework.css', __FILE__ ) );
}
add_action( 'elementor/editor/after_register_styles', 'my_plugin_register_editor_styles' );

function my_plugin_enqueue_editor_styles() {
	wp_enqueue_style( 'editor-style-1' );
	wp_enqueue_style( 'editor-style-2' );
}
add_action( 'elementor/editor/after_enqueue_styles', 'my_plugin_enqueue_editor_styles' );
```
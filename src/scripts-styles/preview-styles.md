---
title: "预览样式"
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

# 预览样式

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

当你开发扩展 [Elementor 预览](src/editor/elementor-preview) 的插件，并且需要注册自定义样式表时，请使用 `elementor/preview/enqueue_styles` 动作钩子。该钩子在 Elementor 预览样式被注册和入队时触发。

## 注册预览样式

在下面的示例中，我们将在 Elementor 预览样式被注册和入队后，注册并加入自定义样式表：

```php {6,12}
function my_plugin_register_preview_styles() {
	wp_register_style( 'preview-style-1', plugins_url( 'assets/css/preview-style-1.css', __FILE__ ) );
	wp_register_style( 'preview-style-2', plugins_url( 'assets/css/preview-style-2.css', __FILE__ ), [ 'external-framework' ] );
	wp_register_style( 'external-framework', plugins_url( 'assets/css/libs/external-framework.css', __FILE__ ) );
}
add_action( 'wp_enqueue_scripts', 'my_plugin_register_preview_styles' );

function my_plugin_enqueue_preview_styles() {
	wp_enqueue_style( 'preview-style-1' );
	wp_enqueue_style( 'preview-style-2' );
}
add_action( 'elementor/preview/enqueue_styles', 'my_plugin_enqueue_preview_styles' );
```
---
title: "预览脚本"
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

# 预览脚本

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

当你开发扩展 [Elementor 预览](src/editor/elementor-preview) 的插件并需要注册自定义脚本时，请使用 `elementor/preview/enqueue_scripts` 动作钩子，该钩子在预览脚本注册和入队时触发。

## 注册预览脚本

在下面的示例中，我们将在 Elementor 脚本注册和入队后，注册并入队自定义脚本：

```php {6,12}
function my_plugin_register_preview_scripts() {
	wp_register_script( 'preview-script-1', plugins_url( 'assets/js/preview-script-1.js', __FILE__ ) );
	wp_register_script( 'preview-script-2', plugins_url( 'assets/js/preview-script-2.js', __FILE__ ), [ 'external-library' ] );
	wp_register_script( 'external-library', plugins_url( 'assets/js/libs/external-library.js', __FILE__ ) );
}
add_action( 'wp_enqueue_scripts', 'my_plugin_register_preview_scripts' );

function my_plugin_enqueue_preview_scripts() {
	wp_enqueue_script( 'preview-script-1' );
	wp_enqueue_script( 'preview-script-2' );
}
add_action( 'elementor/preview/enqueue_scripts', 'my_plugin_enqueue_preview_scripts' );
```
---
title: "Widget Dependencies"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Widgets
    - Src
    - Repos
---

# Widget Dependencies

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Some widgets are dependent on custom scripts for functionality and custom styles for look and feel. Widgets can use external JS libraries, CSS frameworks, or custom JS handlers. Let's see how to use them.

## 定义依赖项

在 widget 类中，我们可以通过以下方式定义所需的 JS 和 CSS 依赖项：

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function get_script_depends(): array {
		return [ 'script-handle' ];
	}

	public function get_style_depends(): array {
		return [ 'style-handle' ];
	}

}
```

*   **脚本依赖项** – `get_script_depends()` 方法允许您定义运行 widget 所需的 JS 文件。

*   **样式依赖项** – `get_style_depends()` 方法允许您定义运行 widget 所需的 CSS 文件。

请注意，这些依赖项应该已经注册。widget 类仅告知 Elementor 它需要加载哪些依赖项。

## 在 WordPress 中注册脚本与样式

与其他 WordPress 插件一样，脚本和样式必须在插件的 PHP 文件中使用 [wp_register_script()](https://developer.wordpress.org/reference/functions/wp_register_script/) 和 [wp_register_style()](https://developer.wordpress.org/reference/functions/wp_register_style/) 函数进行注册。

WordPress 提供了多个钩子来注册脚本/样式，具体取决于它们的使用位置：

* [wp_enqueue_scripts](https://developer.wordpress.org/reference/hooks/wp_enqueue_scripts/) - 用于前端页面脚本和样式的钩子
* [login_enqueue_scripts](https://developer.wordpress.org/reference/hooks/login_enqueue_scripts/) - 用于登录页面脚本和样式的钩子
* [admin_enqueue_scripts](https://developer.wordpress.org/reference/hooks/admin_enqueue_scripts/) - 用于管理页面脚本和样式的钩子

## Registering Scripts & Styles in Elementor

Elementor addon developers should register JS and CSS dependencies in the main file, usually where [widgets are registered](src/widgets/add-new-widget):

```php
/**
 * Register Elementor test widgets.
 */
function elementor_test_widgets_registration( $widgets_manager ) {

	require_once( __DIR__ . '/widgets/test-widget-1.php' );
	require_once( __DIR__ . '/widgets/test-widget-2.php' );

	$widgets_manager->register( new \Elementor_Test_Widget_1() );
	$widgets_manager->register( new \Elementor_Test_Widget_2() );

}
add_action( 'elementor/widgets/register', 'elementor_test_widgets_registration' );

/**
 * Register scripts and styles for Elementor test widgets.
 */
function elementor_test_widgets_dependencies() {

	/* Scripts */
	wp_register_script( 'widget-script-1', plugins_url( 'assets/js/widget-script-1.js', __FILE__ ) );
	wp_register_script( 'widget-script-2', plugins_url( 'assets/js/widget-script-2.js', __FILE__ ), [ 'external-library' ] );
	wp_register_script( 'external-library', plugins_url( 'assets/js/libs/external-library.js', __FILE__ ) );

	/* Styles */
	wp_register_style( 'widget-style-1', plugins_url( 'assets/css/widget-style-1.css', __FILE__ ) );
	wp_register_style( 'widget-style-2', plugins_url( 'assets/css/widget-style-2.css', __FILE__ ), [ 'external-framework' ] );
	wp_register_style( 'external-framework', plugins_url( 'assets/css/libs/external-framework.css', __FILE__ ) );

}
add_action( 'wp_enqueue_scripts', 'elementor_test_widgets_dependencies' );
```

Then, each widgets should set its dependencies as follows:

```php
class Elementor_Test_Widget_1 extends \Elementor\Widget_Base {

	public function get_script_depends(): array {
		return [ 'external-library' ];
	}

	public function get_style_depends(): array {
		return [ 'external-framework' ];
	}

}
```

```php
class Elementor_Test_Widget_2 extends \Elementor\Widget_Base {

	public function get_script_depends(): array {
		return [ 'widget-script-1', 'widget-script-2' ];
	}

	public function get_style_depends(): array {
		return [ 'widget-style-1', 'widget-style-2' ];
	}

}
```

This way, Elementor can build the dependency tree and enqueue only dependencies for widgets used in the page.

### 使用 Elementor 资源

第三方开发者可以使用 Elementor 注册的资源，例如使用 [Swiper](https://swiperjs.com/) 创建基于轮播的小部件。

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function get_style_depends(): array {
		return [ 'swiper', 'widget-custom-style' ];
	}

	public function get_script_depends(): array {
		return [ 'swiper', 'widget-custom-script' ];
	}

}
```

Elementor 为其轮播小部件注册了 swiper，Elementor Pro 和许多其他 Elementor 插件都使用它，而不是注册自己的库版本。

### 使用 Elementor 脚本

要使用不同的 Elementor JS 方法，小部件需要声明 `elementor-frontend` 作为依赖项：

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function get_script_depends(): array {
		return [ 'elementor-frontend', 'widget-custom-script' ];
	}

}
```

当第三方小部件注册自己的前端处理程序时，这会非常方便。在 [controls `frontend_available` 参数](src/editor-controls/frontend-available) 中了解更多信息。
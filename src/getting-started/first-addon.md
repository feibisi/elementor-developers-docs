---
title: "创建您的首个扩展插件"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Getting Started
    - Src
    - Repos
---

# 创建您的首个扩展插件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

让我们创建一个简单的 Elementor 扩展插件，为 Elementor 添加两个小部件。第一个将是简单的 "Hello World" 小部件，而第二个将与之类似，但功能有所增强。

## 插件文件夹结构

第一步将是注册这两个小部件。

插件应放置在您网站的 `wp-content/plugins/` 文件夹中，文件夹结构如下所示：

```
elementor-addon/
|
├─ widgets/
|  ├─ hello-world-widget-1.php
|  └─ hello-world-widget-2.php
|
└─ elementor-addon.php
```

您可以将整个 `elementor-addon` 文件夹压缩，然后从“_WordPress 仪表盘_” > “_插件_”页面将 `zip` 文件上传到您的网站。

## 插件文件

这些小组件需要多个文件。主文件 `elementor-addon.php` 将用于注册小组件。`hello-world-widget-1.php` 和 `hello-world-widget-2.php` 文件将控制小组件的功能：

### The Main Addon File

**elementor-addon.php**

```php
<?php
/**
 * Plugin Name: Elementor Addon
 * Description: Simple hello world widgets for Elementor.
 * Version:     1.0.0
 * Author:      Elementor Developer
 * Author URI:  https://developers.elementor.com/
 * Text Domain: elementor-addon
 *
 * Requires Plugins: elementor
 * Elementor tested up to: 3.25.0
 * Elementor Pro tested up to: 3.25.0
 */

function register_hello_world_widget( $widgets_manager ) {

	require_once( __DIR__ . '/widgets/hello-world-widget-1.php' );
	require_once( __DIR__ . '/widgets/hello-world-widget-2.php' );

	$widgets_manager->register( new \Elementor_Hello_World_Widget_1() );
	$widgets_manager->register( new \Elementor_Hello_World_Widget_2() );

}
add_action( 'elementor/widgets/register', 'register_hello_world_widget' );
```

Header comments are the standard way WordPress uses to provide information about plugins:

<img :src="$withBase('/assets/img/elementor-addon-plugin-screen.png')" alt="Plugins screen">

Elementor register new widgets with the widget registration function. Here, we will use the `elementor/widgets/register` lifecycle hook to run the `register_hello_world_widget()` function.

The function first loads the two widget files and then registers the widget classes using the widget manager. After running the code, the widget panel will display the two widgets:

<img :src="$withBase('/assets/img/elementor-addon-widgets.png')" alt="The two widgets in the widgets panel">

### 第一个小部件

第一个小部件是 `widgets/hello-world-widget-1.php`。它非常简单，只是在屏幕上打印文本 "Hello World"。使用以下代码创建它：

```php
<?php
class Elementor_Hello_World_Widget_1 extends \Elementor\Widget_Base {

	public function get_name(): string {
		return 'hello_world_widget_1';
	}

	public function get_title(): string {
		return esc_html__( 'Hello World 1', 'elementor-addon' );
	}

	public function get_icon(): string {
		return 'eicon-code';
	}

	public function get_categories(): array {
		return [ 'basic' ];
	}

	public function get_keywords(): array {
		return [ 'hello', 'world' ];
	}

	protected function render(): void {
		?>
		<p> Hello World </p>
		<?php
	}

	protected function content_template(): void {
		?>
		<p> Hello World </p>
		<?php
	}
}
```

### The Second Widget

The second widget is `widgets/hello-world-widget-2.php`. It creates two controls in the widget panel. One allows the user to enter their own text and style the text with a custom color (with "Hello World" being the default text). Create it using the following code:

```php
<?php
class Elementor_Hello_World_Widget_2 extends \Elementor\Widget_Base {

	public function get_name(): string {
		return 'hello_world_widget_2';
	}

	public function get_title(): string {
		return esc_html__( 'Hello World 2', 'elementor-addon' );
	}

	public function get_icon(): string {
		return 'eicon-code';
	}

	public function get_categories(): array {
		return [ 'basic' ];
	}

	public function get_keywords(): array {
		return [ 'hello', 'world' ];
	}

	protected function register_controls(): void {

		// Content Tab Start

		$this->start_controls_section(
			'section_title',
			[
				'label' => esc_html__( 'Title', 'elementor-addon' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'title',
			[
				'label' => esc_html__( 'Title', 'elementor-addon' ),
				'type' => \Elementor\Controls_Manager::TEXTAREA,
				'default' => esc_html__( 'Hello world', 'elementor-addon' ),
			]
		);

		$this->end_controls_section();

		// Content Tab End


		// Style Tab Start

		$this->start_controls_section(
			'section_title_style',
			[
				'label' => esc_html__( 'Title', 'elementor-addon' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_control(
			'title_color',
			[
				'label' => esc_html__( 'Text Color', 'elementor-addon' ),
				'type' => \Elementor\Controls_Manager::COLOR,
				'selectors' => [
					'{{WRAPPER}} .hello-world' => 'color: {{VALUE}};',
				],
			]
		);

		$this->end_controls_section();

		// Style Tab End

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['title'] ) ) {
			return;
		}
		?>
		<p class="hello-world">
			<?php echo $settings['title']; ?>
		</p>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.title ) {
			return;
		}
		#>
		<p class="hello-world">
			{{ settings.title }}
		</p>
		<?php
	}
}
```

Now that you’ve seen how easy it is to create your first Elementor addon, it’s time to take advantage of the growing Elementor market and start working on your own cool ideas.

Continue reading more about [Building Advanced Addons](src/addons) with best practices, coding standards and even more [code examples](src/addons/addon-example).
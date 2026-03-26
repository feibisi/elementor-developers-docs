---
title: "复杂示例"
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

# 复杂示例

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

为展示复杂动态标签，我们将允许用户从可用服务器变量列表中显示服务器变量。它将包含一个自定义的[动态标签组](src/dynamic-tags/dynamic-tags-groups)，并提供一个包含所有可用服务器变量的选择框控件。渲染函数将返回用户选择的变量及其值。

## 文件夹结构

该插件将包含两个文件。动态标签及其功能文件。主文件将注册标签和标签组。

```
elementor-server-variable-dynamic-tag/
|
├─ dynamic-tags/
|  └─ server-variable-dynamic-tag.php
|
└─ elementor-server-variable-dynamic-tag.php
```

## Plugin Files

**elementor-server-variable-dynamic-tag.php**

```php
<?php
/**
 * Plugin Name: Elementor Server Variable Dynamic Tag
 * Description: Add dynamic tag that returns an server variable.
 * Plugin URI:  https://elementor.com/
 * Version:     1.0.0
 * Author:      Elementor Developer
 * Author URI:  https://developers.elementor.com/
 * Text Domain: elementor-server-variable-dynamic-tag
 *
 * Requires Plugins: elementor
 * Elementor tested up to: 3.25.0
 * Elementor Pro tested up to: 3.25.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Register Request Variables Dynamic Tag Group.
 *
 * Register new dynamic tag group for Request Variables.
 *
 * @since 1.0.0
 * @param \Elementor\Core\DynamicTags\Manager $dynamic_tags_manager Elementor dynamic tags manager.
 * @return void
 */
function register_request_variables_dynamic_tag_group( $dynamic_tags_manager ) {

	$dynamic_tags_manager->register_group(
		'request-variables',
		[
			'title' => esc_html__( 'Request Variables', 'textdomain' )
		]
	);

}
add_action( 'elementor/dynamic_tags/register', 'register_request_variables_dynamic_tag_group' );

/**
 * Register Server Variable Dynamic Tag.
 *
 * Include dynamic tag file and register tag class.
 *
 * @since 1.0.0
 * @param \Elementor\Core\DynamicTags\Manager $dynamic_tags_manager Elementor dynamic tags manager.
 * @return void
 */
function register_server_variable_dynamic_tag( $dynamic_tags_manager ) {

	require_once( __DIR__ . '/dynamic-tags/server-variable-dynamic-tag.php' );

	$dynamic_tags_manager->register( new \Elementor_Dynamic_Tag_Server_Variable );

}
add_action( 'elementor/dynamic_tags/register', 'register_server_variable_dynamic_tag' );
```

**dynamic-tags/server-variable-dynamic-tag.php**

```php
<?php
if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Elementor Dynamic Tag - Server Variable
 *
 * Elementor dynamic tag that returns a server variable.
 *
 * @since 1.0.0
 */
class Elementor_Dynamic_Tag_Server_Variable extends \Elementor\Core\DynamicTags\Tag {

	/**
	 * Get dynamic tag name.
	 *
	 * Retrieve the name of the server variable tag.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string Dynamic tag name.
	 */
	public function get_name(): string {
		return 'server-variable';
	}

	/**
	 * Get dynamic tag title.
	 *
	 * Returns the title of the server variable tag.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string Dynamic tag title.
	 */
	public function get_title(): string {
		return esc_html__( 'Server Variable', 'textdomain' );
	}

	/**
	 * Get dynamic tag groups.
	 *
	 * Retrieve the list of groups the server variable tag belongs to.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return array Dynamic tag groups.
	 */
	public function get_group(): array {
		return [ 'request-variables' ];
	}

/**
	 * 获取动态标签分类。
	 *
	 * 检索服务器变量标签所属的分类列表。
	 *
	 * @since 1.0.0
	 * @access public
	 * @return array 动态标签分类。
	 */
	public function get_categories(): array {
		return [ \Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY ];
	}

	/**
	 * 注册动态标签控件。
	 *
	 * 添加输入字段，允许用户自定义服务器变量标签设置。
	 *
	 * @since 1.0.0
	 * @access protected
	 * @return void
	 */
	protected function register_controls(): void {
		$variables = [];

		foreach ( array_keys( $_SERVER ) as $variable ) {
			$variables[ $variable ] = ucwords( str_replace( '_', ' ', $variable ) );
		}

		$this->add_control(
			'user_selected_variable',
			[
				'type' => \Elementor\Controls_Manager::SELECT,
				'label' => esc_html__( '变量', 'textdomain' ),
				'options' => $variables,
			]
		);
	}

	/**
	 * 在前端渲染标签输出。
	 *
	 * 用 PHP 编写，用于生成最终的 HTML。
	 *
	 * @since 1.0.0
	 * @access public
	 * @return void
	 */
	public function render(): void {
		$user_selected_variable = $this->get_settings( 'user_selected_variable' );

		if ( ! $user_selected_variable ) {
			return;
		}

		if ( ! isset( $_SERVER[ $user_selected_variable ] ) ) {
			return;
		}

		$value = $_SERVER[ $user_selected_variable ];
		echo wp_kses_post( $value );
	}

}
```

## The Result

The dynamic tag in a group view:

<img :src="$withBase('/assets/img/elementor-dynamic-tag-example-server-variable-groups.png')" alt="Dynamic tag example - groups">

The dynamic tag controls:

<img :src="$withBase('/assets/img/elementor-dynamic-tag-example-server-variable-controls.png')" alt="Dynamic tag example - controls">
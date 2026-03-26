---
title: "简单示例"
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

# 简单示例

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

总而言之，我们将创建一个返回随机数的简单动态标签。为简化示例，此动态标签不包含控件。但您可以扩展代码，添加最小值和最大值的限制控件。

## 文件夹结构

该插件将包含两个文件。动态标签及其功能文件，主文件将用于注册标签。

```
elementor-random-number-dynamic-tag/
|
├─ dynamic-tags/
|  └─ random-number-dynamic-tag.php
|
└─ elementor-random-number-dynamic-tag.php
```

## Plugin Files

**elementor-random-number-dynamic-tag.php**

```php
<?php
/**
 * Plugin Name: Elementor Random Number Dynamic Tag
 * Description: Add dynamic tag that returns a random number.
 * Plugin URI:  https://elementor.com/
 * Version:     1.0.0
 * Author:      Elementor Developer
 * Author URI:  https://developers.elementor.com/
 * Text Domain: elementor-random-number-dynamic-tag
 *
 * Requires Plugins: elementor
 * Elementor tested up to: 3.25.0
 * Elementor Pro tested up to: 3.25.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Register Random Number Dynamic Tag.
 *
 * Include dynamic tag file and register tag class.
 *
 * @since 1.0.0
 * @param \Elementor\Core\DynamicTags\Manager $dynamic_tags_manager Elementor dynamic tags manager.
 * @return void
 */
function register_random_number_dynamic_tag( $dynamic_tags_manager ) {

	require_once( __DIR__ . '/dynamic-tags/random-number-dynamic-tag.php' );

	$dynamic_tags_manager->register( new \Elementor_Dynamic_Tag_Random_Number );

}
add_action( 'elementor/dynamic_tags/register', 'register_random_number_dynamic_tag' );
```

**dynamic-tags/random-number-dynamic-tag.php**

```php
<?php
if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Elementor Dynamic Tag - Random Number
 *
 * Elementor dynamic tag that returns a random number.
 *
 * @since 1.0.0
 */
class Elementor_Dynamic_Tag_Random_Number extends \Elementor\Core\DynamicTags\Tag {

	/**
	 * Get dynamic tag name.
	 *
	 * Retrieve the name of the random number tag.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string Dynamic tag name.
	 */
	public function get_name(): string {
		return 'random-number';
	}

	/**
	 * Get dynamic tag title.
	 *
	 * Returns the title of the random number tag.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string Dynamic tag title.
	 */
	public function get_title(): string {
		return esc_html__( 'Random Number', 'elementor-random-number-dynamic-tag' );
	}

	/**
	 * Get dynamic tag groups.
	 *
	 * Retrieve the list of groups the random number tag belongs to.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return array Dynamic tag groups.
	 */
	public function get_group(): array {
		return [ 'actions' ];
	}

	/**
	 * Get dynamic tag categories.
	 *
	 * Retrieve the list of categories the random number tag belongs to.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return array Dynamic tag categories.
	 */
	public function get_categories(): array {
		return [ \Elementor\Modules\DynamicTags\Module::NUMBER_CATEGORY ];
	}

	/**
	 * Render tag output on the frontend.
	 *
	 * Written in PHP and used to generate the final HTML.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return void
	 */
	public function render(): void {
		echo rand();
	}

}
```
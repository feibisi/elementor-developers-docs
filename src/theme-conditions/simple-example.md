---
title: "简单示例"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Theme Conditions
    - Src
    - Repos
---

# 简单示例

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

为演示扩展主题条件是多么简单，我们将创建一个插件来注册一个条件，用于检查访问者是否已登录。该插件将帮助 Elementor 用户向已登录访问者显示某些模板，而向匿名访问者显示其他模板。

## 文件夹结构

该插件将包含两个文件。一个文件用于处理已登录用户条件，另一个主文件则负责注册该条件并处理所有其他功能。

```
elementor-logged-in-user-condition/
|
├─ theme-conditions/
|  └─ logged-in-user-condition.php
|
└─ elementor-logged-in-user-condition.php
```

## Plugin Files

**elementor-logged-in-user-condition.php**

```php
<?php
/**
 * Plugin Name: Elementor Logged-In User Condition
 * Description: Custom addon that adds a logged-in user condition to Elementor.
 * Plugin URI:  https://elementor.com/
 * Version:     1.0.0
 * Author:      Elementor Developer
 * Author URI:  https://developers.elementor.com/
 * Text Domain: elementor-logged-in-user-condition
 *
 * Requires Plugins: elementor
 * Elementor tested up to: 3.25.0
 * Elementor Pro tested up to: 3.25.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Add a logged-in user condition to Elementor.
 *
 * @since 1.0.0
 * @param \ElementorPro\Modules\ThemeBuilder\Classes\Conditions_Manager $conditions_manager An instance of conditions manager.
 * @return void
 */
function add_new_logged_in_user_condition( $conditions_manager ) {

	require_once( __DIR__ . '/theme-conditions/logged-in-user-condition.php' );

	$conditions_manager->get_condition( 'general' )->register_sub_condition( new \Logged_In_User_Condition() );

}
add_action( 'elementor/theme/register_conditions', 'add_new_logged_in_user_condition' );
```

**theme-conditions/logged-in-user-condition.php**

```php
<?php
if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Elementor Logged-In User Condition.
 *
 * Add a logged-in user condition to Elementor.
 *
 * @since 1.0.0
 */
class Logged_In_User_Condition extends \ElementorPro\Modules\ThemeBuilder\Conditions\Condition_Base {

	/**
	 * Get condition group type.
	 *
	 * Retrieve logged-in user condition group type.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public static function get_type(): string {
		return 'general';
	}

	/**
	 * Get condition name.
	 *
	 * Retrieve logged-in user condition unique ID.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public function get_name(): string {
		return 'logged_in_user';
	}

	/**
	 * Get condition label.
	 *
	 * Retrieve logged-in user condition label.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public function get_label(): string {
		return esc_html__( 'Logged-in user', 'elementor-logged-in-user-condition' );
	}

	/**
	 * Check condition.
	 *
	 * Validate logged-in user condition to ensure it complies with certain rules.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return bool
	 */
	public function check( $args ): bool {
		return is_user_logged_in();
	}

}
```

## The Result

The "Logged-In User" condition as displayed on the conditions screen:

<img :src="$withBase('/assets/img/elementor-theme-conditions-example-logged-in-user.png')" alt="Logged-In User Condition">
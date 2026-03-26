---
title: "进阶示例"
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

# 进阶示例

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

针对更高级的用例，我们将创建一个插件，根据已登录访问者的角色来注册条件。该插件将帮助 Elementor 用户仅向具有特定角色的访问者显示某些模板。

## 文件夹结构

该插件将包含三个文件。两个文件用于条件设置，主文件用于注册条件并处理所有其他事项。

```
elementor-user-role-conditions/
|
├─ theme-conditions/
|  ├─ logged-in-user-condition.php
|  └─ user-role-condition.php
|
└─ elementor-user-role-conditions.php
```

## Plugin Files

**elementor-user-role-conditions.php**

```php
<?php
/**
 * Plugin Name: Elementor User Role Conditions
 * Description: Custom addon that adds user role conditions to Elementor.
 * Plugin URI:  https://elementor.com/
 * Version:     1.0.0
 * Author:      Elementor Developer
 * Author URI:  https://developers.elementor.com/
 * Text Domain: elementor-user-role-conditions
 *
 * Requires Plugins: elementor
 * Elementor tested up to: 3.25.0
 * Elementor Pro tested up to: 3.25.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Add user role conditions to Elementor.
 *
 * @since 1.0.0
 * @param \ElementorPro\Modules\ThemeBuilder\Classes\Conditions_Manager $conditions_manager An instance of conditions manager.
 * @return void
 */
function add_new_user_role_conditions( $conditions_manager ) {

	require_once( __DIR__ . '/theme-conditions/logged-in-user-condition.php' );
	require_once( __DIR__ . '/theme-conditions/user-role-condition.php' );

	$conditions_manager->get_condition( 'general' )->register_sub_condition( new \Logged_In_User_Condition() );
}
add_action( 'elementor/theme/register_conditions', 'add_new_user_role_conditions' );
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
		return esc_html__( 'Logged-in User', 'elementor-user-role-conditions' );
	}

	/**
	 * Get condition all label.
	 *
	 * Retrieve logged-in user condition 'All' label.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public function get_all_label(): string {
		return esc_html__( 'Any user role', 'elementor-user-role-conditions' );
	}

	/**
	 * Register sub-conditions.
	 *
	 * Add sub-conditions based on user role.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return void
	 */
	public function register_sub_conditions(): void {
		global $wp_roles;

		if ( ! isset( $wp_roles ) ) {
			$wp_roles = new \WP_Roles();
		}

		$user_roles_list = $wp_roles->get_names();

		foreach ( $user_roles_list as $role ) {
			$this->register_sub_condition( new \User_Role_Condition( $role ) );
		}
	}

/**
	 * Check condition.
	 *
	 * Validate logged-in user condition to ensure it complies to certain rules.
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

**theme-conditions/user-role-condition.php**

```php
<?php
if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Elementor User Role Conditions.
 *
 * Add a user role conditions to Elementor.
 *
 * @since 1.0.0
 */
class User_Role_Condition extends \ElementorPro\Modules\ThemeBuilder\Conditions\Condition_Base {

	/**
	 * Condition constructor.
	 *
	 * Initialize user role condition.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public function __construct( $user_role ) {
		parent::__construct();

		$this->user_role = $user_role;
	}

	/**
	 * Get condition group type.
	 *
	 * Retrieve user role condition group type.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public static function get_type(): string {
		return 'logged_in_user';
	}

	/**
	 * Get condition name.
	 *
	 * Retrieve user role condition unique ID.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public function get_name(): string {
		return strtolower( $this->user_role . '_role' );
	}

	/**
	 * Get condition label.
	 *
	 * Retrieve user role condition label.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return string
	 */
	public function get_label(): string {
		/* translators: %s: User role label. */
		return sprintf( esc_html__( '%s role', 'elementor-user-role-conditions' ), $this->user_role );
	}

	/**
	 * Check condition.
	 *
	 * Validate user role condition to ensure it complies to certain rules.
	 *
	 * @since 1.0.0
	 * @access public
	 * @return bool
	 */
	public function check( $args ): bool {
		$current_user = wp_get_current_user();
		$site_roles = (array) $current_user->roles;
		return in_array( $this->user_role, $site_roles );
	}

}
```

## The Result

The "Logged-In User" > "User Roles" conditions:

<img :src="$withBase('/assets/img/elementor-theme-conditions-example-user-roles.png')" alt="User role conditions">

The "User Roles" list:

<img :src="$withBase('/assets/img/elementor-theme-conditions-example-user-roles-list.png')" alt="The list of user roles">
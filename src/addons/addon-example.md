---
title: "插件包装器示例"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Addons
    - Src
    - Repos
---

# 插件包装器示例

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

让我们为 Elementor 插件创建一个包装器，它整合了目前所学的所有内容——文件/文件夹结构、每个 WordPress 插件所需的基本头部注释、命名空间以及兼容性检查。

## 文件夹结构

该插件将采用以下文件夹结构：

```
elementor-test-addon/
|
├─ includes/
|  |
|  ├─ controls/
|  |  ├─ control-1.php
|  |  └─ control-2.php
|  |
|  ├─ widgets/
|  |  ├─ widget-1.php
|  |  └─ widget-2.php
|  |
|  └─ plugin.php
|
└─ elementor-test-addon.php
```

## The Entire Code

The addon code should look as follows:

**elementor-test-addon.php**

```php
<?php
/**
 * Plugin Name: Elementor Test Addon
 * Description: Custom Elementor addon.
 * Plugin URI:  https://elementor.com/
 * Version:     1.0.0
 * Author:      Elementor Developer
 * Author URI:  https://developers.elementor.com/
 * Text Domain: elementor-test-addon
 *
 * Requires Plugins: elementor
 * Elementor tested up to: 3.25.0
 * Elementor Pro tested up to: 3.25.0
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

function elementor_test_addon() {

	// Load plugin file
	require_once( __DIR__ . '/includes/plugin.php' );

	// Run the plugin
	\Elementor_Test_Addon\Plugin::instance();

}
add_action( 'plugins_loaded', 'elementor_test_addon' );
```

**includes/plugin.php**

```php
namespace Elementor_Test_Addon;

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

/**
 * Plugin class.
 *
 * The main class that initiates and runs the addon.
 *
 * @since 1.0.0
 */
final class Plugin {

	/**
	 * Addon Version
	 *
	 * @since 1.0.0
	 * @var string The addon version.
	 */
	const VERSION = '1.0.0';

	/**
	 * Minimum Elementor Version
	 *
	 * @since 1.0.0
	 * @var string Minimum Elementor version required to run the addon.
	 */
	const MINIMUM_ELEMENTOR_VERSION = '3.20.0';

	/**
	 * Minimum PHP Version
	 *
	 * @since 1.0.0
	 * @var string Minimum PHP version required to run the addon.
	 */
	const MINIMUM_PHP_VERSION = '7.4';

	/**
	 * Instance
	 *
	 * @since 1.0.0
	 * @access private
	 * @static
	 * @var \Elementor_Test_Addon\Plugin The single instance of the class.
	 */
	private static $_instance = null;

	/**
	 * Instance
	 *
	 * Ensures only one instance of the class is loaded or can be loaded.
	 *
	 * @since 1.0.0
	 * @access public
	 * @static
	 * @return \Elementor_Test_Addon\Plugin An instance of the class.
	 */
	public static function instance() {

		if ( is_null( self::$_instance ) ) {
			self::$_instance = new self();
		}
		return self::$_instance;

	}

	/**
	 * Constructor
	 *
	 * Perform some compatibility checks to make sure basic requirements are meet.
	 * If all compatibility checks pass, initialize the functionality.
	 *
	 * @since 1.0.0
	 * @access public
	 */
	public function __construct() {

		if ( $this->is_compatible() ) {
			add_action( 'elementor/init', [ $this, 'init' ] );
		}

	}

	/**
	 * Compatibility Checks
	 *
	 * Checks whether the site meets the addon requirement.
	 *
	 * @since 1.0.0
	 * @access public
	 */
	public function is_compatible(): void {

		// Check if Elementor installed and activated
		if ( ! did_action( 'elementor/loaded' ) ) {
			add_action( 'admin_notices', [ $this, 'admin_notice_missing_main_plugin' ] );
			return false;
		}

		// Check for required Elementor version
		if ( ! version_compare( ELEMENTOR_VERSION, self::MINIMUM_ELEMENTOR_VERSION, '>=' ) ) {
			add_action( 'admin_notices', [ $this, 'admin_notice_minimum_elementor_version' ] );
			return false;
		}

// Check for required PHP version
		if ( version_compare( PHP_VERSION, self::MINIMUM_PHP_VERSION, '<' ) ) {
			add_action( 'admin_notices', [ $this, 'admin_notice_minimum_php_version' ] );
			return false;
		}

		return true;

	}

	/**
	 * Admin notice
	 *
	 * Warning when the site doesn't have Elementor installed or activated.
	 *
	 * @since 1.0.0
	 * @access public
	 */
	public function admin_notice_missing_main_plugin(): void {

		if ( isset( $_GET['activate'] ) ) unset( $_GET['activate'] );

		$message = sprintf(
			/* translators: 1: Plugin name 2: Elementor */
			esc_html__( '"%1$s" requires "%2$s" to be installed and activated.', 'elementor-test-addon' ),
			'<strong>' . esc_html__( 'Elementor Test Addon', 'elementor-test-addon' ) . '</strong>',
			'<strong>' . esc_html__( 'Elementor', 'elementor-test-addon' ) . '</strong>'
		);

		printf( '<div class="notice notice-warning is-dismissible"><p>%1$s</p></div>', $message );

	}

	/**
	 * Admin notice
	 *
	 * Warning when the site doesn't have a minimum required Elementor version.
	 *
	 * @since 1.0.0
	 * @access public
	 */
	public function admin_notice_minimum_elementor_version(): void {

		if ( isset( $_GET['activate'] ) ) unset( $_GET['activate'] );

		$message = sprintf(
			/* translators: 1: Plugin name 2: Elementor 3: Required Elementor version */
			esc_html__( '"%1$s" requires "%2$s" version %3$s or greater.', 'elementor-test-addon' ),
			'<strong>' . esc_html__( 'Elementor Test Addon', 'elementor-test-addon' ) . '</strong>',
			'<strong>' . esc_html__( 'Elementor', 'elementor-test-addon' ) . '</strong>',
			 self::MINIMUM_ELEMENTOR_VERSION
		);

		printf( '<div class="notice notice-warning is-dismissible"><p>%1$s</p></div>', $message );

	}

	/**
	 * Admin notice
	 *
	 * Warning when the site doesn't have a minimum required PHP version.
	 *
	 * @since 1.0.0
	 * @access public
	 */
	public function admin_notice_minimum_php_version(): void {

		if ( isset( $_GET['activate'] ) ) unset( $_GET['activate'] );

		$message = sprintf(
			/* translators: 1: Plugin name 2: PHP 3: Required PHP version */
			esc_html__( '"%1$s" requires "%2$s" version %3$s or greater.', 'elementor-test-addon' ),
			'<strong>' . esc_html__( 'Elementor Test Addon', 'elementor-test-addon' ) . '</strong>',
			'<strong>' . esc_html__( 'PHP', 'elementor-test-addon' ) . '</strong>',
			 self::MINIMUM_PHP_VERSION
		);

		printf( '<div class="notice notice-warning is-dismissible"><p>%1$s</p></div>', $message );

	}

	/**
	 * Initialize
	 *
	 * Load the addons functionality only after Elementor is initialized.
	 *
	 * Fired by `elementor/init` action hook.
	 *
	 * @since 1.0.0
	 * @access public
	 */
	public function init(): void {

		add_action( 'elementor/widgets/register', [ $this, 'register_widgets' ] );
		add_action( 'elementor/controls/register', [ $this, 'register_controls' ] );

	}

/**
	 * 注册小工具
	 *
	 * 加载小工具文件并注册新的 Elementor 小工具。
	 *
	 * 由 `elementor/widgets/register` 动作钩子触发。
	 *
	 * @param \Elementor\Widgets_Manager $widgets_manager Elementor 小工具管理器。
	 */
	public function register_widgets( $widgets_manager ): void {

		require_once( __DIR__ . '/includes/widgets/widget-1.php' );
		require_once( __DIR__ . '/includes/widgets/widget-2.php' );

		$widgets_manager->register( new Widget_1() );
		$widgets_manager->register( new Widget_2() );

	}

	/**
	 * 注册控件
	 *
	 * 加载控件文件并注册新的 Elementor 控件。
	 *
	 * 由 `elementor/controls/register` 动作钩子触发。
	 *
	 * @param \Elementor\Controls_Manager $controls_manager Elementor 控件管理器。
	 */
	public function register_controls( $controls_manager ): void {

		require_once( __DIR__ . '/includes/controls/control-1.php' );
		require_once( __DIR__ . '/includes/controls/control-2.php' );

		$controls_manager->register( new Control_1() );
		$controls_manager->register( new Control_2() );

	}

}
```
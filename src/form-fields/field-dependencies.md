---
title: "字段依赖关系"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Form Fields
    - Src
    - Repos
---

# 字段依赖关系

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

某些表单字段的功能依赖于自定义脚本，外观则依赖于自定义样式。让我们看看如何设置字段依赖关系。

## 依赖属性

在字段类内部，我们可以通过以下方式声明所需的任何 JS 或 CSS 依赖：

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function get_script_depends(): array {
		return [ 'script-handle' ];
	}

	public function get_style_depends(): array {
		return [ 'style-handle' ];
	}

}
```

* **字段脚本** – `get_script_depends()` 方法定义了显示字段所需的 JS 文件。

* **字段样式** – `get_style_depends()` 方法定义了显示字段所需的 CSS 文件。

## 在 WordPress 中注册脚本与样式

与其他 WordPress 插件一样，脚本和样式必须在插件的 PHP 文件中使用 [wp_register_script()](https://developer.wordpress.org/reference/functions/wp_register_script/) 和 [wp_register_style()](https://developer.wordpress.org/reference/functions/wp_register_style/) 函数进行注册。

你可以使用 [wp_enqueue_scripts](https://developer.wordpress.org/reference/hooks/wp_enqueue_scripts/) 钩子在前端页面注册脚本和样式。

## Registering Scripts & Styles in Elementor

Elementor addon developers should register JS and CSS dependencies in the main file, usually where [form fields are registered](src/form-fields/add-new-field):

```php
/**
 * Register Elementor form fields.
 */
function elementor_test_field_registration( $form_fields_registrar ) {

	require_once( __DIR__ . '/forms/fields/field-1.php' );
	require_once( __DIR__ . '/forms/fields/field-2.php' );

	$form_fields_registrar->register( new \Elementor_Test_Field_1() );
	$form_fields_registrar->register( new \Elementor_Test_Field_2() );

}
add_action( 'elementor_pro/forms/fields/register', 'elementor_test_field_registration' );

/**
 * Register scripts and styles for Elementor form fields.
 */
function elementor_test_field_dependencies() {

	/* Scripts */
	wp_register_script( 'field-script', plugins_url( 'assets/js/field-script.js', __FILE__ ) );
	wp_register_script( 'external-library', plugins_url( 'assets/js/libs/external-library.js', __FILE__ ) );

	/* Styles */
	wp_register_style( 'field-style', plugins_url( 'assets/css/field-style.css', __FILE__ ) );
	wp_register_style( 'external-framework', plugins_url( 'assets/css/libs/external-framework.css', __FILE__ ) );

}
add_action( 'wp_enqueue_scripts', 'elementor_test_field_dependencies' );
```

Then, each form field should set its dependencies as follows:

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function get_script_depends(): array {
		return [ 'field-script', 'external-library' ];
	}

	public function get_style_depends(): array {
		return [ 'field-style', 'external-framework' ];
	}

}
```

## 向后兼容性

在 Elementor 3.28 版本之前，依赖声明通过 `$depended_scripts` 和 `$depended_styles` 属性实现：

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public $depended_scripts = [ 'script-handle' ];

	public $depended_styles = [ 'style-handle' ];

}
```

如需支持 3.28 之前的 Elementor 版本，请将这些属性添加到表单字段类中，并配置所需的脚本/样式句柄。
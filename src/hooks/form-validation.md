---
title: "表单验证"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Hooks
    - Src
    - Repos
---

# 表单验证

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

表单验证允许您运行一系列检查，以确保数据符合特定规则。Elementor Pro 提供了一套工具，用于验证通过表单小部件发送的数据。

## 验证生命周期

当表单模块加载完成且为包含表单操作的 POST 请求时，此处可添加表单验证处理器。

## 验证钩子

Elementor Pro 提供以下操作钩子来验证表单数据：

* `elementor_pro/forms/validation`
* `elementor_pro/forms/validation/{$field_type}`

第一个钩子应用于所有字段，第二个钩子应用于特定的[字段类型](src/form-fields)。

## Examples

Validating email field:

```php
function elementor_form_email_field_validation( $field, $record, $ajax_handler ) {
	// Validate email format
	if ( ! is_email( $field['value'] ) ) {
		$ajax_handler->add_error( $field['id'], esc_html__( 'Invalid email address, it must be in xx@xx.xx format.', 'textdomain' ) );
		return;
	}

	// Do your validation here.
}
add_action( 'elementor_pro/forms/validation/email', 'elementor_form_email_field_validation', 10, 3 );
```

Validate the Ticket ID field is in XXX-XXXX format:

```php
function elementor_form_validation( $record, $ajax_handler ) {
	$fields = $record->get_field( [
		'id' => 'ticket_id',
	] );

	if ( empty( $fields ) ) {
		return;
	}

	$field = current( $fields );

	if ( 1 !== preg_match( '/^\w{3}-\w{4}$/', $field['value'] ) ) {
		$ajax_handler->add_error( $field['id'], esc_html__( 'Invalid Ticket ID, it must be in XXX-XXXX format.', 'textdomain' ) );
	}
}
add_action( 'elementor_pro/forms/validation', 'elementor_form_validation', 10, 2 );
```

Tel match this format XXX-XXX-XXXX, i.e. 123-456-7890

```php
function elementor_form_tel_field_validation( $field, $record, $ajax_handler ) {
	// Remove native validation
	$forms_module = \ElementorPro\Plugin::instance()->modules_manager->get_modules( 'forms' );
	remove_action( 'elementor_pro/forms/validation/tel', [ $forms_module->fields_registrar->get( 'tel' ), 'validation' ], 10, 3 );

	// Run your own validation, ex:
	if ( empty( $field['value'] ) ) {
		return;
	}

	// Match this format XXX-XXX-XXXX, e.g. 123-456-7890
	if ( preg_match( '/[0-9]{3}(-?)[0-9]{3}(-?)[0-9]{4}/', $field['value'] ) !== 1 ) {
		$ajax_handler->add_error( $field['id'], esc_html__( 'Please make sure the phone number is in XXX-XXX-XXXX format, eg: 123-456-7890', 'textdomain' ) );
	}
}
add_action( 'elementor_pro/forms/validation/tel', 'elementor_form_tel_field_validation', 10, 3 );

function elementor_form_tel_field_rendering( $item, $item_index, $form ) {
	// Remove native render
	$forms_module = \ElementorPro\Plugin::instance()->modules_manager->get_modules( 'forms' );
	remove_action( 'elementor_pro/forms/render_field/tel', [ $forms_module->fields_registrar->get( 'tel' ), 'field_render' ], 10, 3 );

	// Add custom render ex:
	$form->add_render_attribute( 'input' . $item_index, 'class', 'elementor-field-textual' );
	$form->add_render_attribute( 'input' . $item_index, 'pattern', '[0-9]{3}(-?)[0-9]{3}(-?)[0-9]{4}' );
	$form->add_render_attribute( 'input' . $item_index, 'title', esc_html__( 'Number should be in this format xxx-xxx-xxxx.', 'textdomain' ) );

	echo '<input size="1" ' . $form->get_render_attribute_string( 'input' . $item_index ) . '>';
}
add_action( 'elementor_pro/forms/render_field/tel', 'elementor_form_tel_field_rendering', 9, 3 );
```
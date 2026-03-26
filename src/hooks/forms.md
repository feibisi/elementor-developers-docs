---
title: "Elementor Forms"
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

# Elementor Forms

::: danger
This page will be deleted once all the content will be moved to individual pages inside [Elementor Hooks](src/hooks).
:::

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

<img :src="$withBase('/assets/img/elementor-form.png')" alt="Elementor Form Widget" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

**Elementor Form Builder** is an advanced [Elementor Widget](src/widgets) that allows users to create forms with the ultimate drag and drop visual form builder.

[[toc]]

## 概述

表单 API 是一组特定功能，允许开发者扩展 Elementor 表单功能。

外部开发者可以扩展表单小部件功能以满足自身需求。例如：以新方式验证数据、集成新的营销自动化工具和 CRM 服务、在保存或发送前修改收集的数据等。

## 表单钩子

**[Elementor Pro](https://elementor.com/pro/)** 为核心 Elementor 添加了新功能。表单 API 允许开发者过滤内容、验证数据、修改网络钩子、执行自定义代码等。

### 表单验证

#### `elementor_pro/forms/validation`

在表单模块加载后，并且这是一个包含表单操作的 POST 请求时。这是添加表单验证处理程序的地方。

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `record` | `Form_Record` | The record submitted. |
| `ajax_handler` | `Ajax_Handler` | The Ajax Handler component. |

##### Example

```php
// Validate the Ticket ID field is in XXX-XXXX format.
add_action( 'elementor_pro/forms/validation', function ( $record, $ajax_handler ) {
	$fields = $record->get_field( [
		'id' => 'ticket_id',
	] );

	if ( empty( $fields ) ) {
		return;
	}

	$field = current( $fields );

	if ( 1 !== preg_match( '/^\w{3}-\w{4}$/', $field['value'] ) ) {
		$ajax_handler->add_error( $field['id'], 'Invalid Ticket ID, it must be in the format XXX-XXXX' );
	}
}, 10, 2 );
```

#### `elementor_pro/forms/validation/{$field_type}`

在表单模块加载后，且为包含表单操作的 POST 请求时触发。此钩子允许开发者验证单个字段类型。

钩子名称的动态部分 `$field_type` 指代字段类型。

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `field` | `Array` | The submitted field. |
| `record` | `Form_Record` | The record submitted. |
| `ajax_handler` | `Ajax_Handler` | The Ajax Handler component. |

##### Example

```php
// Validate the Tel field is in XXX-XXX-XXXX format.
add_action( 'elementor_pro/forms/validation/tel', function( $field, $record, $ajax_handler ) {

	// Match this format XXX-XXX-XXXX, 123-456-7890

	if ( preg_match( '/[0-9]{3}-[0-9]{3}-[0-9]{4}/', $field['value'] ) !== 1 ) {
		$ajax_handler->add_error( $field['id'], 'Please make sure the phone number is in XXX-XXX-XXXX format, eg: 123-456-7890' );
	}
}, 10, 3 );
```

### 表单处理

#### `elementor_pro/forms/process`

在表单字段验证和处理完成后触发。这是添加额外表单字段处理工作处理程序的地方。

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `record` | `Form_Record` | The record submitted. |
| `ajax_handler` | `Ajax_Handler` | The Ajax Handler component. |

#### `elementor_pro/forms/process/{$field_type}`

在表单字段验证通过后，当处理单个表单字段时触发。这允许开发者处理特定的字段类型。

钩子名称的动态部分 `$field_type` 指代字段类型。

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `field` | `Array` | The submitted field. |
| `record` | `Form_Record` | The record submitted. |
| `ajax_handler` | `Ajax_Handler` | The Ajax Handler component. |

### 表单提交

#### `elementor_pro/forms/form_submitted`

在表单模块加载后，且为包含表单操作的 POST 请求时触发。此处用于添加表单处理器。

##### 参数

| 参数 | 类型 | 描述 |
|----------|------|-------------|
| `module` | `ElementorPro\Modules\Forms` | 当前页面/文章的完整 Elementor HTML 输出。 |

##### 示例

```php
add_action( 'elementor_pro/forms/form_submitted', function( $module ) {
	$module->add_component( 'uploads_handler', new Uploads_Handler() );
} );
```

### 创建新记录

#### `elementor_pro/forms/new_record`

在表单操作运行后触发。此处用于添加自定义表单处理程序。

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `record` | `Form_Record` | The record submitted. |
| `ajax_handler` | `Ajax_Handler` | The Ajax Handler component. |

##### Example

```php
function send_custom_webhook( $record, $handler ) {

	$form_name = $record->get_form_settings( 'form_name' );

	// Replace MY_FORM_NAME with the name you gave your form
	if ( 'MY_FORM_NAME' !== $form_name ) {
		return;
	}

	$raw_fields = $record->get( 'fields' );
	$fields = [];
	foreach ( $raw_fields as $id => $field ) {
		$fields[ $id ] = $field['value'];
	}

	wp_remote_post(
		'https://api.example.com/',
		[
			'body' => $fields,
		]
	);
}
add_action( 'elementor_pro/forms/new_record', 'send_custom_webhook', 10, 2 );
```

### 表单 Webhooks 响应

#### `elementor_pro/forms/webhooks/response`

处理 Webhook 响应。

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `response` | `array/WP_Error` | The `wp_remote_post response`. See [wp\_remote\_retrieve\_response\_message()](https://developer.wordpress.org/reference/functions/wp_remote_retrieve_response_code/) function for more information |
| `record` | `Form_Record` | The record submitted. |

### 表单邮件头过滤器

#### `elementor_pro/forms/wp_mail_headers`

##### 参数

| 参数 | 类型 | 描述 |
|----------|------|-------------|
| `headers` | `string` | 用于 `wp_mail` 参数的电子邮件头信息。 |

### 表单邮件消息过滤器

#### `elementor_pro/forms/wp_mail_message`

##### 参数

| 参数 | 类型 | 描述 |
|----------|------|-------------|
| `email_text` | `string` | 用于 `wp_mail` 参数的电子邮件 HTML 内容。 |

### 邮件发送成功后的操作

#### `elementor_pro/forms/mail_sent`

##### Arguments

| Argument | Type | Description |
|----------|------|-------------|
| `settings` | `array` | The form settings. |
| `record` | `Form_Record` | The record submitted. |
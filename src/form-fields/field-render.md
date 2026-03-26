---
title: "字段渲染"
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

# 字段渲染

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

表单中使用的字段需要在前端有输出。渲染方法用于设置字段在网站前端向用户显示时的代码。

## 渲染方法

实际生成字段输出的方法称为 `render()`。在你的字段类中，按如下方式使用此方法：

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function render( $item, $item_index, $form ): void {

		echo '<input type="text" class="elementor-test-field" title="Some text...">';

	}

}
```

* **字段渲染** – `render()` 方法渲染数据并显示字段输出。

## 渲染属性

要以“Elementor 的方式”添加属性，不应将 HTML 元素与属性硬编码。应使用 `add_render_attribute()` 方法。此方法负责以编程方式定义属性及其值。

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function render( $item, $item_index, $form ): void {
		$form->add_render_attribute(
			'input' . $item_index,
			[
				'type'        => 'text',
				'class'       => 'elementor-test-field',
				'placeholder' => esc_html__( 'Some placeholder', 'textdomain' ),
			]
		);

		echo '<input ' . $form->get_render_attribute_string( 'input' . $item_index ) . '>';
	}

}
```

## 从字段控件获取数据

某些字段具有[自定义控件](src/form-fields/field-controls)，允许用户自定义字段。在表单小部件中显示用户数据的方式如下：

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function render( $item, $item_index, $form ): void {
		$form->add_render_attribute(
			'textarea' . $item_index,
			[
				'class' => 'elementor-test-field',
				'rows'  => $item['textarea-rows'],
				'cols'  => $item['textarea-cols'],
			]
		);

		echo '<textarea ' . $form->get_render_attribute_string( 'textarea' . $item_index ) . '></textarea>';
	}

}
```
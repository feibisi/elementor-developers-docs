---
title: "字段控件"
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

# 字段控件

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

表单字段可以拥有额外的控件，允许用户自定义表单字段。当字段被添加到表单时，这些控件将显示在字段设置中。输入到这些控件中的数据会被保存到数据库，之后可用于渲染字段输出或验证字段值。

## 注册控件

在您的字段类中，可以使用 `update_controls()` 方法添加控件，如下所示：

```php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function update_controls( $widget ): void {

		/* ... */

	}

}
```

* **字段控件** – `update_controls()` 方法用于更新小部件控件，它允许开发者向特定字段类型添加新控件。`$widget` 参数是表单小部件的一个实例。

## 向字段添加控件

在下面的示例中，我们将向小部件实例添加一些控件，以允许用户自定义表单字段：

```php {13-36}
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function update_controls( $widget ): void {

		$elementor = \ElementorPro\Plugin::elementor();

		$control_data = $elementor->controls_manager->get_control_from_stack( $widget->get_unique_name(), 'form_fields' );

		if ( is_wp_error( $control_data ) ) {
			return;
		}

		$field_controls = [
			'first-control' => [
				'name' => 'first-control',
				'label' => esc_html__( 'First Control', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'condition' => [
					'field_type' => $this->get_type(),
				],
				'tab'          => 'content',
				'inner_tab'    => 'form_fields_content_tab',
				'tabs_wrapper' => 'form_fields_tabs',
			],
			'second-control' => [
				'name' => 'second-control',
				'label' => esc_html__( 'Second Control', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'condition' => [
					'field_type' => $this->get_type(),
				],
				'tab'          => 'content',
				'inner_tab'    => 'form_fields_content_tab',
				'tabs_wrapper' => 'form_fields_tabs',
			],
		];

		$control_data['fields'] = $this->inject_field_controls( $control_data['fields'], $field_controls );

		$widget->update_control( 'form_fields', $control_data );

	}

}
```

本质上，我们是在向表单小部件中注入新的字段控件。这些字段被注入到“*字段重复器*”中，用户在此处向表单添加字段。

`$control_data` 是表单小部件内部的字段重复器。此代码注入了新的字段，并设置了显示条件，使其仅在特定字段类型和字段内容选项卡中显示。

<img :src="$withBase('/assets/img/elementor-form-field-controls.png')" alt="Elementor Form - Field Controls">
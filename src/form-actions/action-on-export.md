---
title: "导出时的处理"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Form Actions
    - Src
    - Repos
---

# 导出时的处理

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

最佳实践是在导出 Elementor 数据时排除操作设置。如果你的表单操作添加了一些设置（[操作控件](src/form-actions/action-controls)），则不应导出它们。

## 导出方法

用于从导出过程中排除数据的方法称为 `on_export()`。此方法可用于在导出时排除操作数据。

```php
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function on_export( $element ): array {

		return $element;

	}

}
```

* **导出时** - `on_export()` 方法用于在导出时清除设置。`$element` 参数是一个包含导出元素数据的数组。

## 排除设置

在以下示例中，我们将注册一个包含两个控件的新部分——一个 API 密钥和一个应用 ID。然后我们将它们从导出的数据中排除：

```php {16,24,35-44}
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function register_settings_section( $widget ): void {

		$widget->start_controls_section(
			'custom_action_section',
			[
				'label' => esc_html__( 'Custom Action', 'textdomain' ),
				'condition' => [
					'submit_actions' => $this->get_name(),
				],
			]
		);

		$widget->add_control(
			'custom_action_api_key',
			[
				'label' => esc_html__( 'API Key', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
			]
		);

		$widget->add_control(
			'custom_action_app_id',
			[
				'label' => esc_html__( 'App ID', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
			]
		);

		$widget->end_controls_section();

	}

	public function on_export( $element ): array {

		unset(
			$element['custom_action_api_key'],
			$element['custom_action_app_id'],
		);

		return $element;

	}

}
```
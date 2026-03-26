---
title: "组合控制"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor Controls
    - Src
    - Repos
---

# 组合控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

组合控制是一组具有相似功能的[常规控件](src/editor-controls/regular-control)和[响应式控件](src/editor-controls/responsive-control)，它们被组合成一个单一控件（例如：排版控制、文本阴影控制、盒阴影控制）。要添加组合控件，我们使用 `add_group_control()` 方法。

## 分组控件结构

使用以下代码添加分组控件：

```php
$this->add_group_control(
	Group_Control_Class::get_type(),
	[
		'name' => 'control_name',
		'label' => esc_html__( '内容', 'textdomain' ),
	]
);
```

## 控制参数

每个控件包含以下关键参数：

* **组控件类型** `(string)` – 组控件的唯一名称。
* **组控件设置** `(array)` – 额外的控制参数。除基于控件类型的默认设置外，每个控件还有其专属的*自定义设置*。例如，"exclude" 设置可用于从组中排除某些内部控件。

## 示例

### 版式控制

当向 Elementor 小部件添加标题和自定义内容时，我们需要允许用户设计文本样式。我们可以使用 `Group_Control_Typography` 类中定义的版式控制来设置字体大小、字体系列、字体粗细、文本转换、字体样式、行高和字母间距。

```php {13-19}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_group_control(
			\Elementor\Group_Control_Typography::get_type(),
			[
				'name' => 'title_typography',
				'selector' => '{{WRAPPER}} .title',
			]
		);

		$this->end_controls_section();

	}

}
```

### 边框控制

边框控制与排版控制略有不同。它通过 `Group_Control_Border` 类来定义，用于设置边框类型、边框宽度和边框颜色：

```php {13-19}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_group_control(
			\Elementor\Group_Control_Border::get_type(),
			[
				'name' => 'border',
				'selector' => '{{WRAPPER}} .wrapper',
			]
		);

		$this->end_controls_section();

	}

}
```

### Group Control Fields Options

Here's an advanced setup for changing inner controls inside the group control using `fields_options`:

```php {13-40}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls() {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_group_control(
			\Elementor\Group_Control_Border::get_type(),
			[
				'name' => 'box_border',
				'label' => esc_html__( 'Box Border', 'textdomain' ),
				'fields_options' => [
					'border' => [
						'label' => esc_html__( 'Box Border Type', 'textdomain' ),
						'default' => 'solid',
					],
					'width' => [
						'label' => esc_html__( 'Box Border Width', 'textdomain' ),
						'default' => [
							'top' => '1',
							'right' => '2',
							'bottom' => '3',
							'left' => '4',
							'isLinked' => false,
						],
					],
					'color' => [
						'label' => esc_html__( 'Box Border Color', 'textdomain' ),
						'default' => '#D4D4D4',
					],
				],
				'selector' => '{{WRAPPER}} .some-box',
			]
		);

		$this->end_controls_section();

	}

}
```
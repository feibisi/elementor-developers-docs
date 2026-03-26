---
title: "Popover Toggle Control"
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

# Popover Toggle Control

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-popover-toggle.png')" alt="Popover Toggle Control" style="float: right;">

Elementor popover toggle control displays a toggle  button to open and close a popover. The control allow you to open a popover with custom controls.

<img :src="$withBase('/assets/img/controls/control-popover-toggle-active.png')" alt="Acvite Popover Toggle Control" style="float: right;">

The control is defined in `Control_Popover_Toggle` class which extends `Base_Data_Control` class.

When using this control, the `type` should be set to `\Elementor\Controls_Manager::POPOVER_TOGGLE` constant.

## 参数

<table>
	<thead>
		<tr>
			<th>名称</th>
			<th>类型</th>
			<th>默认值</th>
			<th>描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>type</code></td>
			<td><code>string</code></td>
			<td>popover_toggle</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>label</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在字段上方的标签。</td>
		</tr>
		<tr>
			<td><code>description</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在字段下方的描述。</td>
		</tr>
		<tr>
			<td><code>show_label</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>是否显示标签。</td>
		</tr>
		<tr>
			<td><code>label_block</code></td>
			<td><code>bool</code></td>
			<td>false</td>
			<td>是否在单独一行显示标签。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>label_on</code></td>
			<td><code>string</code></td>
			<td>Custom</td>
			<td>“未选中”状态的标签。</td>
		</tr>
		<tr>
			<td><code>label_off</code></td>
			<td><code>string</code></td>
			<td>Default</td>
			<td>“选中”状态的标签。</td>
		</tr>
		<tr>
			<td><code>return_value</code></td>
			<td><code>string</code></td>
			<td>yes</td>
			<td>选中时返回的值。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>字段的默认值。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`_) The popover toggle field value, based on `return_value` argument.

## Usage

```php {14-24,26,34}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_control(
			'border_popover_toggle',
			[
				'label' => esc_html__( 'Border', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::POPOVER_TOGGLE,
				'label_off' => esc_html__( 'Default', 'textdomain' ),
				'label_on' => esc_html__( 'Custom', 'textdomain' ),
				'return_value' => 'yes',
				'default' => 'yes',
			]
		);

		$this->start_popover();

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_popover();

		$this->end_controls_section();

	}

}
```
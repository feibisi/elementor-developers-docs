---
title: "选择控件"
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

# 选择控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-select.png')" alt="Select Control" style="float: right;">

Elementor 选择控件显示一个简单的下拉选择框。它接受一个数组，其中 `key` 是选项的 `value`，而值则是选项名称。

该控件定义在继承 `Base_Data_Control` 类的 `Control_Select` 类中。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::SELECT` 常量。

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
			<td>select</td>
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
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>options</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>一个 <code>键 =&gt; 值</code> 对的数组：<code>[ '键' =&gt; '值', ... ]</code></td>
		</tr>
		<tr>
			<td><code>groups</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>分组选项的数组。</td>
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

(_`string`_) The selected option value.

## Usage

```php {14-32,34-67,76-78,84-86}
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
			'border_style',
			[
				'label' => esc_html__( 'Border Style', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::SELECT,
				'default' => 'solid',
				'options' => [
					'' => esc_html__( 'Default', 'textdomain' ),
					'none' => esc_html__( 'None', 'textdomain' ),
					'solid'  => esc_html__( 'Solid', 'textdomain' ),
					'dashed' => esc_html__( 'Dashed', 'textdomain' ),
					'dotted' => esc_html__( 'Dotted', 'textdomain' ),
					'double' => esc_html__( 'Double', 'textdomain' ),
				],
				'selectors' => [
					'{{WRAPPER}} .your-class' => 'border-style: {{VALUE}};',
				],
			]
		);

		$this->add_control(
			'custom_animation',
			[
				'label' => esc_html__( 'Animation', 'textdomain' ),
				'type' => Controls_Manager::SELECT,
				'groups' => [
					[
						'label' => esc_html__( 'None', 'textdomain' ),
						'options' => [
							'' => esc_html__( 'None', 'textdomain' ),
						],
					],
					[
						'label' => esc_html__( 'Slide', 'textdomain' ),
						'options' => [
							'slide-from-right' => esc_html__( 'Slide In Right', 'textdomain' ),
							'slide-from-left' => esc_html__( 'Slide In Left', 'textdomain' ),
							'slide-from-top' => esc_html__( 'Slide In Up', 'textdomain' ),
							'slide-from-bottom' => esc_html__( 'Slide In Down', 'textdomain' ),
						],
					],
					[
						'label' => esc_html__( 'Zoom', 'textdomain' ),
						'options' => [
							'grow' => esc_html__( 'Grow', 'textdomain' ),
							'shrink' => esc_html__( 'Shrink', 'textdomain' ),
							'zoom-in' => esc_html__( 'Zoom In', 'textdomain' ),
							'zoom-out' => esc_html__( 'Zoom Out', 'textdomain' ),
						],
					],
				],
				'prefix_class' => 'custom-animation-',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		?>
		<div class="your-class">
			...
		</div>
		<?php
	}

	protected function content_template(): void {
		?>
		<div class="your-class">
			...
		</div>
		<?php
	}

}
```
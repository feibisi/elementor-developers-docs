---
title: "视觉选择控件"
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

# 视觉选择控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-visual-choice.png')" alt="Visual Choice Control" style="float: right;">

Elementor 视觉选择控件将单选按钮显示为带图像的按钮组。

该控件定义在继承 `Base_Data_Control` 类的 `Control_Visual_Choice` 类中。

使用此控件时，`type` 应设置为 `\Elementor\Controls_Manager::VISUAL_CHOICE` 常量。

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
			<td>visual_choice</td>
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
			<td>true</td>
			<td>是否在单独一行显示标签。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>options</code></td>
			<td><code>array</code></td>
			<td>[]</td>
			<td>一个多维数组，包含每个单选按钮的 <code>title</code> 和 <code>image</code>。
		</tr>
		<tr>
			<td><code>columns</code></td>
			<td><code>number</code></td>
			<td>1</td>
			<td>网格布局中的列数。</td>
		</tr>
		<tr>
			<td><code>toggle</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>是否允许切换/取消选择。</td>
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

```php {14-50}
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
			'structure',
			[
				'label' => esc_html__( 'Structure', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::VISUAL_CHOICE,
				'label_block' => true,
				'options' => [
					'grid-3' => [
						'title' => esc_attr__( 'Grid: 3 columns.', 'textdomain' ),
						'image' => plugins_url( 'assets/img/grid-3.svg', __FILE__ ),
					],
					'masonry' => [
						'title' => esc_attr__( 'Masonry: arbitrary order', 'textdomain' ),
						'image' => plugins_url( 'assets/img/masonry.svg', __FILE__ ),
					],
					'stacked' => [
						'title' => esc_attr__( 'Stacked: Single column.', 'textdomain' ),
						'image' => plugins_url( 'assets/img/stacked.svg', __FILE__ ),
					],
					'focus' => [
						'title' => esc_attr__( 'Focus: Text only.', 'textdomain' ),
						'image' => plugins_url( 'assets/img/focus.svg', __FILE__ ),
					],
					'grid-2' => [
						'title' => esc_attr__( 'Grid: 2 columns.', 'textdomain' ),
						'image' => plugins_url( 'assets/img/grid2.svg', __FILE__ ),
					],
					'stretch' => [
						'title' => esc_attr__( 'Stretch: fit available width.', 'textdomain' ),
						'image' => plugins_url( 'assets/img/stretch.svg', __FILE__ ),
					]
				],
				'default' => 'masonry',
				'columns' => 2,
				'prefix_class' => 'some-layout-',
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
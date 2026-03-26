---
title: "滑块控件"
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

# 滑块控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-slider.png')" alt="Slider Control" style="float: right;">

Elementor 滑块控件显示一个可拖动的范围滑块。该控件可选择性地包含多种单位类型 (`size_units`) 供用户选择。控件还接受一个 `range` 参数，允许您为每种单位类型设置 `min`、`max` 和 `step` 值。

<img :src="$withBase('/assets/img/controls/control-slider2.png')" alt="Slider Control" style="float: right;">

此控件在继承 `Control_Base_Units` 类的 `Control_Slider` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::SLIDER` 常量。

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
			<td>slider</td>
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
			<td><code>size_units</code></td>
			<td><code>array</code></td>
			<td>[ 'px' ]</td>
			<td>可用 CSS 单位的数组，例如 <code>px</code>、<code>em</code>、<code>rem</code>、<code>%</code>、<code>deg</code>、<code>vh</code> 或 <code>custom</code>。</td>
		</tr>
		<tr>
			<td><code>range</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				每个注册尺寸的范围数组。
				<ul>
					<li><strong>$min</strong> (<code>int</code>) 范围的最小值。</li>
					<li><strong>$max</strong> (<code>int</code>) 范围的最大值。</li>
					<li><strong>$step</strong> (<code>int</code>) 使用控件微调器时递增或递减的间隔值。</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				滑块默认值。
				<ul>
					<li><strong>$unit</strong> (<code>string</code>) 滑块的初始单位。</li>
					<li><strong>$size</strong> (<code>int</code>) 滑块的初始尺寸。</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## 返回值

```
[
	'unit' => '',
	'size' => '',
]
```

(_`array`_) 一个包含尺寸值的数组：

*   **$unit** (_`string`_) 选定的单位。
*   **$size** (_`int`_) 选定的尺寸。

## 用法

```php {14-39,48-50,56-58}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'width',
			[
				'label' => esc_html__( 'Width', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::SLIDER,
				'size_units' => [ 'px', '%', 'em', 'rem', 'custom' ],
				'range' => [
					'px' => [
						'min' => 0,
						'max' => 1000,
						'step' => 5,
					],
					'%' => [
						'min' => 0,
						'max' => 100,
					],
				],
				'default' => [
					'unit' => '%',
					'size' => 50,
				],
				'selectors' => [
					'{{WRAPPER}} .your-class' => 'width: {{SIZE}}{{UNIT}};',
				],
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
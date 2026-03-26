---
title: "尺寸控制"
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

# 尺寸控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-dimensions.png')" alt="Dimensions Control" style="float: right;">

Elementor 尺寸控制显示上、右、下、左的输入字段，并提供将它们链接在一起的选项。该控件可选择包含多种单位类型 (`size_units`) 供用户选择。它还接受 `range` 参数，允许您为每种单位类型设置 `min`、`max` 和 `step` 值。

<img :src="$withBase('/assets/img/controls/control-dimensions2.png')" alt="Dimensions Control" style="float: right;">

该控件在继承 `Control_Base_Units` 类的 `Control_Dimensions` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::DIMENSIONS` 常量。

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
			<td>dimensions</td>
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
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				滑块默认值。
				<ul>
					<li><strong>$top</strong> (<code>int</code>) 顶部尺寸的初始大小。</li>
					<li><strong>$right</strong> (<code>int</code>) 右侧尺寸的初始大小。</li>
					<li><strong>$bottom</strong> (<code>int</code>) 底部尺寸的初始大小。</li>
					<li><strong>$left</strong> (<code>int</code>) 左侧尺寸的初始大小。</li>
					<li><strong>$unit</strong> (<code>string</code>) CSS 单位类型的初始大小。</li>
					<li><strong>$isLinked</strong> (<code>bool</code>) 是否将所有值链接在一起。</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><code>placeholder</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				当字段没有值时显示的占位符。
				<ul>
					<li><strong>$top</strong> (<code>int</code>) 顶部尺寸的占位符。</li>
					<li><strong>$right</strong> (<code>int</code>) 右侧尺寸的占位符。</li>
					<li><strong>$bottom</strong> (<code>int</code>) 底部尺寸的占位符。</li>
					<li><strong>$left</strong> (<code>int</code>) 左侧尺寸的占位符。</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## 返回值

```
[
	'top' => '',
	'right' => '',
	'bottom' => '',
	'left' => '',
	'unit' => '',
	'isLinked' => '',
]
```

(_`array`_) 包含尺寸值的数组：

*   **$top** (_`int`_) 顶部尺寸。
*   **$right** (_`int`_) 右侧尺寸。
*   **$bottom** (_`int`_) 底部尺寸。
*   **$left** (_`int`_) 左侧尺寸。
*   **$unit** (_`string`_) CSS 单位类型。
*   **$isLinked** (_`bool`_) 是否将所有值链接在一起。

## Usage

```php {14-32,41-43,49-51}
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
			'margin',
			[
				'label' => esc_html__( 'Margin', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::DIMENSIONS,
				'size_units' => [ 'px', '%', 'em', 'rem', 'custom' ],
				'default' => [
					'top' => 2,
					'right' => 0,
					'bottom' => 2,
					'left' => 0,
					'unit' => 'em',
					'isLinked' => false,
				],
				'selectors' => [
					'{{WRAPPER}} .your-class' => 'margin: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
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
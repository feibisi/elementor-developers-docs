---
title: "文本描边组控件"
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

# 文本描边组控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 文本描边组控件显示用于定义文本描边的输入字段，包括水平描边、垂直描边、描边模糊和描边颜色。

该控件在继承 `Group_Control_Base` 类的 `Group_Control_Text_Stroke` 类中定义。

使用此组控件时，应将 `type` 设置为 `Group_Control_Text_Stroke::get_type()` 方法。

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
			<td>text-stroke</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>exclude</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>从组控件中排除某些控件。示例：<code>['text_stroke']</code></td>
		</tr>
	</tbody>
</table>

## 返回值

(_`array`_) 包含文本描边值的数组。

## 用法

```php {14-20,29-31,37-39}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_group_control(
			\Elementor\Group_Control_Text_Stroke::get_type(),
			[
				'name' => 'text_stroke',
				'selector' => '{{WRAPPER}} .your-class',
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
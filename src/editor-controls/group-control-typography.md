---
title: "排版组控件"
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

# 排版组控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 排版组控件显示用于定义内容排版的输入字段，包括字体大小、字体系列、字体粗细、文本转换、字体样式、行高和字母间距。

该控件在继承 `Group_Control_Base` 类的 `Group_Control_Typography` 类中定义。

使用此组控件时，`type` 应设置为 `Group_Control_Typography::get_type()` 方法。

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
			<td>typography</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>exclude</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>从组控件中排除某些控件。例如：<code>['font_style']</code></td>
		</tr>
	</tbody>
</table>

## 返回值

(_`array`_) 包含排版值的数组。

## 用法

```php {14-20,29-31,37-39}
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

		$this->add_group_control(
			\Elementor\Group_Control_Typography::get_type(),
			[
				'name' => 'content_typography',
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

## 说明

了解如何在您的排版控件上使用在[站点设置](src/editor/site-settings-panel)面板中设置的[全局字体](src/editor-controls/global-style)。
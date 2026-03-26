---
title: "警告控制"
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

# 警告控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-alert.png')" alt="Alert Control" style="float: right;">

Elementor 警告控制根据消息的严重程度，在面板中显示四种类型的警告：信息、成功、警告和危险。

该控件在继承 `Base_UI_Control` 类的 `Control_Alert` 类中定义。

使用此控件时，`type` 应设置为 `\Elementor\Controls_Manager::ALERT` 常量。

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
			<td>alert</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>alert_type</code></td>
			<td><code>string</code></td>
			<td>info</td>
			<td>警告的类型。可用值为 <code>info</code>、<code>success</code>、<code>warning</code> 和 <code>danger</code>。</td>
		</tr>
		<tr>
			<td><code>heading</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在警告上方的标题。</td>
		</tr>
		<tr>
			<td><code>content</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>警告的内容。</td>
		</tr>
	</tbody>
</table>

## 返回值

此控件不返回任何值。

## 用法

```php {14-22}
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
			'custom_panel_alert',
			[
				'type' => \Elementor\Controls_Manager::ALERT,
				'alert_type' => 'warning',
				'heading' => esc_html__( 'Custom Alert', 'textdomain' ),
				'content' => esc_html__( 'Lorem ipsum dolor sit amet consectetur adipisicing elit.', 'textdomain' ) . ' <a href="">' . esc_html__( 'Learn more', 'textdomain' ) . '</a>',
			]
		);

		$this->end_controls_section();

	}

}
```
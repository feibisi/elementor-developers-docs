---
title: "通知控件"
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

# 通知控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-notice.png')" alt="Notice Control" style="float: right;">

Elementor 通知控件根据消息的严重程度，在面板中显示四种类型的通知：信息、成功、警告和危险。

与[警告控件](src/editor-controls/control-alert)不同，通知控件可以选择设置为可关闭，允许用户关闭消息并且不再显示。

该控件在继承 `Base_UI_Control` 类的 `Control_Notice` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::NOTICE` 常量。

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
			<td>notice</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>notice_type</code></td>
			<td><code>string</code></td>
			<td>info</td>
			<td>通知的类型。可用值为 <code>info</code>、<code>success</code>、<code>warning</code> 和 <code>danger</code>。</td>
		</tr>
		<tr>
			<td><code>dismissible</code></td>
			<td><code>bool</code></td>
			<td>false</td>
			<td>允许用户关闭通知。</td>
		</tr>
		<tr>
			<td><code>heading</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在通知上方的标题。</td>
		</tr>
		<tr>
			<td><code>content</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>通知的内容。</td>
		</tr>
	</tbody>
</table>

## 返回值

此控件不返回任何值。

## 用法

```php {14-23}
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
			'custom_panel_notice',
			[
				'type' => \Elementor\Controls_Manager::NOTICE,
				'notice_type' => 'warning',
				'dismissible' => true,
				'heading' => esc_html__( 'Custom Notice', 'textdomain' ),
				'content' => esc_html__( 'Lorem ipsum dolor sit amet consectetur adipisicing elit.', 'textdomain' ),
			]
		);

		$this->end_controls_section();

	}

}
```
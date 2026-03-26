---
title: "按钮控件"
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

# 按钮控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 按钮控件可在面板中显示一个能够触发事件的按钮。

该控件定义在继承 `Base_UI_Control` 类的 `Control_Button` 类中。

使用此控件时，应将 `type` 参数设置为 `\Elementor\Controls_Manager::BUTTON` 常量。

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
			<td>button</td>
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
			<td><code>text</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>按钮文本。</td>
		</tr>
		<tr>
			<td><code>button_type</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>按钮类型。可用值为 <code>default</code>、<code>info</code>、<code>success</code>、<code>warning</code> 和 <code>danger</code>。</td>
		</tr>
		<tr>
			<td><code>event</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>按钮将触发的事件。该事件将通过 <code>elementor.channels.editor.on( event )</code> 触发。</td>
		</tr>
	</tbody>
</table>

## Return Value

This control does not return any value.

## Usage

```php {14-24}
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
			'delete_content',
			[
				'label' => esc_html__( 'Delete Content', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::BUTTON,
				'separator' => 'before',
				'button_type' => 'success',
				'text' => esc_html__( 'Delete', 'textdomain' ),
				'event' => 'namespace:editor:delete',
			]
		);

		$this->end_controls_section();

	}

}
```
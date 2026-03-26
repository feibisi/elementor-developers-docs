---
title: "原始 HTML 控件"
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

# 原始 HTML 控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 原始 HTML 控件在面板中显示 HTML 内容。

该控件在继承 `Base_UI_Control` 类的 `Control_Raw_Html` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::RAW_HTML` 常量。

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
			<td>raw_html</td>
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
			<td><code>raw</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>HTML 标记。</td>
		</tr>
		<tr>
			<td><code>content_classes</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>要添加到控件包装器的 CSS 类。</td>
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
			'important_note',
			[
				'label' => esc_html__( 'Important Note', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::RAW_HTML,
				'raw' => esc_html__( 'A very important message to show in the panel.', 'textdomain' ),
				'content_classes' => 'your-class',
			]
		);

		$this->end_controls_section();

	}

}
```
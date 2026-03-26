---
title: "弃用通知控件"
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

# 弃用通知控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 弃用通知控件在面板中显示一个预格式化的通知，警告该小部件已弃用并应被替换。

该控件在 `Control_Deprecated_Notice` 类中定义，该类继承自 `Base_UI_Control` 类。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::DEPRECATED_NOTICE` 常量。

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
			<td><code>widget</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>小部件名称。</td>
		</tr>
		<tr>
			<td><code>since</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>小部件被弃用的插件版本。</td>
		</tr>
		<tr>
			<td><code>last</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>小部件将被移除的插件版本。</td>
		</tr>
		<tr>
			<td><code>plugin</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>插件的标题。</td>
		</tr>
		<tr>
			<td><code>replacement</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>小部件的替代品。</td>
		</tr>
	</tbody>
</table>

## 返回值

此控件不返回任何值。

## 用法

有两种方式可以为小部件添加弃用通知：

### Using the Regular Add Control

Add a notice warning that the widget is deprecated using the regular `add_control()` method.

```php {14-25}
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
			'deprecated_notice',
			[
				'type' => \Elementor\Controls_Manager::DEPRECATED_NOTICE,
				'widget' => 'your-old-widget',
				'since' => '3.10.0',
				'last' => '3.20.0',
				'plugin' => 'Your Great Plugin',
				'replacement' => 'your-new-widget',
				'content_classes' => 'your-class',
			]
		);

		// Register the rest of the controls as usual.

		$this->end_controls_section();

	}

}
```

### Using a Deprecated Notice Method

Add a notice warning that the widget is deprecated using the `deprecated_notice()` method.

```php {14-19}
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

		$this->deprecated_notice(
			'Your Great Plugin',
			'3.10.0',
			'3.20.0',
			'your-new-widget'
		);

		// Register the rest of the controls as usual.

		$this->end_controls_section();

	}
}
```
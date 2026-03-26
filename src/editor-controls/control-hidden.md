---
title: "隐藏控件"
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

# 隐藏控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 隐藏控件在面板中添加一个隐藏的输入字段。它可用于添加数据，而无需在面板中进行可视化呈现。这意味着 Elementor 用户无法访问此控件。

该控件在继承 `Base_Data_Control` 类的 `Control_Hidden` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::HIDDEN` 常量。

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
			<td>hidden</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>label</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在字段上方的标签。但在这种情况下不会显示。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>字段的默认值。</td>
		</tr>
	</tbody>
</table>

## 返回值

(_`string`_) 隐藏字段的值。

## 用法

```php {14-21,30,36}
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
			'view',
			[
				'label' => esc_html__( 'View', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::HIDDEN,
				'default' => 'traditional',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		?>
		<!-- <?php echo $settings['view']; ?> -->		
		<?php
	}

	protected function content_template(): void {
		?>
		<!-- {{{ settings.view }}} -->
		<?php
	}

}
```
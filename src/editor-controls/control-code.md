---
title: "代码控制"
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

# 代码控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-code.png')" alt="Code Control" style="float: right;">

Elementor 代码控制基于 [Ace 编辑器](https://ace.c9.io/) 显示一个代码编辑器文本区域。它接受一个语言参数来定义编程 `language`，并包含语法高亮器以突出显示代码。

该控件在继承 `Base_Data_Control` 类的 `Control_Code` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::CODE` 常量。

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
			<td>code</td>
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
			<td><code>language</code></td>
			<td><code>string</code></td>
			<td>html</td>
			<td>任何 <a href="https://ace.c9.io/build/kitchen-sink.html" target="_blank" rel="noopener">Ace 编辑器支持的语言</a>。</td>
		</tr>
		<tr>
			<td><code>rows</code></td>
			<td><code>int</code></td>
			<td>10</td>
			<td>行数。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>字段的默认值。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`_) The code field value.

## Usage

```php {14-22,36,50}
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
			'custom_html',
			[
				'label' => esc_html__( 'Custom HTML', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::CODE,
				'language' => 'html',
				'rows' => 20,
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['custom_html'] ) ) {
			return;
		}
		?>
		<div class="your-class">
			<?php echo $settings['custom_html']; ?>
		</div>
		<?php

	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.custom_html ) {
			return;
		}
		#>
		<div class="your-class">
			{{{ settings.custom_html }}}
		</div>
		<?php
	}

}
```
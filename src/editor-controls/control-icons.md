---
title: "图标控件"
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

# 图标控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-icons.png')" alt="Icons Control" style="float: right;">

Elementor 图标控件显示图标选择器。此外，它能够从 Elementor 的“图标库”中选择现有图标，或“上传 SVG”到 WordPress 媒体库。

该控件在继承 `Control_Base_Multiple` 类的 `Control_Icons` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::ICONS` 常量。

## 参数

<table>
	<tbody>
		<tr>
			<td><strong>名称</strong></td>
			<td><strong>类型</strong></td>
			<td><strong>默认值</strong></td>
			<td><strong>描述</strong></td>
		</tr>
		<tr>
			<td><code>type</code></td>
			<td><code>string</code></td>
			<td>icons</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>label</code></td>
			<td><code>string</code></td>
			<td>&nbsp;</td>
			<td>显示在字段上方的标签。</td>
		</tr>
		<tr>
			<td><code>description</code></td>
			<td><code>string</code></td>
			<td>&nbsp;</td>
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
			<td>&nbsp;</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td>&nbsp;</td>
			<td>默认值设置为一个包含值和库的数组。</td>
		</tr>
		<tr>
			<td><code>fa4compatibility</code></td>
			<td><code>string</code></td>
			<td>&nbsp;</td>
			<td>用于从旧的 <a href="./control-icon.html">图标控件</a> 迁移数据，应设置为旧控件的名称。</td>
		</tr>
		<tr>
			<td><code>recommended</code></td>
			<td><code>array</code></td>
			<td>&nbsp;</td>
			<td>用于设置此控件实例的推荐图标。</td>
		</tr>
		<tr>
			<td><code>skin</code></td>
			<td><code>string</code></td>
			<td>media</td>
			<td>用于更改控件的外观。有两个选项：<code>media</code> 或 <code>inline</code>。inline 皮肤的设计基于选择控件。</td>
		</tr>
		<tr>
			<td><code>exclude_inline_options</code></td>
			<td><code>array</code></td>
			<td>&nbsp;</td>
			<td>仅与 <code>inline</code> 皮肤一起使用，用于从内联图标控件的按钮中隐藏一个选项（图标库/SVG）。</td>
		</tr>
	</tbody>
</table>

## Return Value

```
[
	'value' => '',
	'library' => '',
]
```

(_`array`_) An array containing icon data:

* **$value** (_`string`_) Icon value.
* **$library** (_`string`_) Icon library name.

## Usage

```php {22-44,53-55,61-66}
<?php
class Icons_Elementor_Test_Control_Widget extends \Elementor\Widget_Base {

	public function get_name(): string {
		return 'icons_test_widget';
	}

	public function get_title(): string {
		return esc_html__( 'Icons Test Widget', 'textdomain' );
	}

	protected function register_controls(): void {

		$this->start_controls_section(
			'section_icon',
			[
				'label' => esc_html__( 'Icon', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'icon',
			[
				'label' => esc_html__( 'Icon', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::ICONS,
				'default' => [
					'value' => 'fas fa-circle',
					'library' => 'fa-solid',
				],
				'recommended' => [
					'fa-solid' => [
						'circle',
						'dot-circle',
						'square-full',
					],
					'fa-regular' => [
						'circle',
						'dot-circle',
						'square-full',
					],
				],
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		?>
		<div class="my-icon-wrapper">
			<?php \Elementor\Icons_Manager::render_icon( $settings['icon'], [ 'aria-hidden' => 'true' ] ); ?>
		</div>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		const iconHTML = elementor.helpers.renderIcon( view, settings.selected_icon, { 'aria-hidden': true }, 'i' , 'object' );
		#>
		<div class="my-icon-wrapper">
			{{{ iconHTML.value }}}
		</div>
		<?php
	}

}
```
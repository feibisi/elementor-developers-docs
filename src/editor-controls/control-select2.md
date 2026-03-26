---
title: "Select2 控件"
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

# Select2 控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-select2.png')" alt="Select2 Control" style="float: right;">

Elementor select2 控件基于 [Select2](https://select2.org/) 库显示一个选择框控件。它接受一个数组，其中 `key` 是值，`value` 是选项名称。将 `multiple` 设置为 `true` 以允许多值选择。

该控件在继承 `Base_Data_Control` 类的 `Control_Select2` 类中定义。

使用此控件时，`type` 应设置为 `\Elementor\Controls_Manager::SELECT2` 常量。

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
			<td>select2</td>
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
			<td><code>options</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>一个 <code>键 =&gt; 值</code> 对的数组：<code>[ '键' =&gt; '值', ... ]</code></td>
		</tr>
		<tr>
			<td><code>multiple</code></td>
			<td><code>bool</code></td>
			<td>false</td>
			<td>是否允许多值选择。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string|array</code></td>
			<td></td>
			<td>选中的选项键，或者如果 <code>multiple</code>&nbsp;设置为&nbsp;<code>true</code>，则为选中值的数组。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`|`array`_) The selected option key, or an array of selected keys if `multiple` is set to `true`.

## Usage

```php {14-28,36-42,47-53}
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
			'list',
			[
				'label' => esc_html__( 'Show Elements', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::SELECT2,
				'label_block' => true,
				'multiple' => true,
				'options' => [
					'title'  => esc_html__( 'Title', 'textdomain' ),
					'description' => esc_html__( 'Description', 'textdomain' ),
					'button' => esc_html__( 'Button', 'textdomain' ),
				],
				'default' => [ 'title', 'description' ],
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		if ( $settings['list'] ) {
			echo '<ul>';
			foreach ( $settings['list'] as $item ) {
				echo '<li>' . $item . '</li>';
			}
			echo '</ul>';
		}
	}

	protected function content_template(): void {
		?>
		<# if ( settings.list.length ) { #>
			<ul>
			<# _.each( settings.list, function( item ) { #>
				<li>{{{ item }}}</li>
			<# } ) #>
			</ul>
		<# } #>
		<?php
	}

}
```
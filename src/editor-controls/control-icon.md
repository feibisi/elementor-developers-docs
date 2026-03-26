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

::: danger 已弃用
此控件已被弃用，推荐使用新的[图标控件](src/editor-controls/control-icons)。
:::

Elementor 图标控件显示一个基于 [Font Awesome](https://fontawesome.com/) 字体的图标选择框。该控件接受 `include` 或 `exclude` 参数来设置部分图标列表。

该控件定义在继承 `Base_Data_Control` 类的 `Control_Icon` 类中。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::ICON` 常量。

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
			<td>icon</td>
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
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>options</code></td>
			<td><code>array</code></td>
			<td><code>get_icons()</code></td>
			<td>可用图标的关联数组。</td>
		</tr>
		<tr>
			<td><code>include</code></td>
			<td><code>array</code></td>
			<td>&nbsp;</td>
			<td>要包含在选项列表中的图标类名数组。</td>
		</tr>
		<tr>
			<td><code>exclude</code></td>
			<td><code>array</code></td>
			<td>&nbsp;</td>
			<td>要从选项列表中排除的图标类名数组。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td>&nbsp;</td>
			<td>默认图标名称。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`_) The selected icon CSS class.

## Usage

```php {14-34,43,49}
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
			'icon',
			[
				'label' => esc_html__( 'Social Icons', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::ICON,
				'include' => [
					'fa fa-facebook',
					'fa fa-flickr',
					'fa fa-google-plus',
					'fa fa-instagram',
					'fa fa-linkedin',
					'fa fa-pinterest',
					'fa fa-reddit',
					'fa fa-twitch',
					'fa fa-twitter',
					'fa fa-vimeo',
					'fa fa-youtube',
				],
				'default' => 'fa fa-facebook',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		?>
		<i class="<?php echo esc_attr( $settings['icon'] ); ?>" aria-hidden="true"></i>
		<?php
	}

	protected function content_template(): void {
		?>
		<i class="{{ settings.icon }}" aria-hidden="true"></i>
		<?php
	}

}
```
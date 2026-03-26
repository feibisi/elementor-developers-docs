---
title: "URL 控件"
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

# URL 控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-url.png')" alt="URL Control" style="float: right;">

Elementor URL 控件显示一个 URL 输入字段。该控件还能够显示更多控制选项，例如在新窗口中打开链接、添加 `nofollow` 属性以及定义额外属性（以逗号分隔的键值对列表）。

<img :src="$withBase('/assets/img/controls/control-url-options2.png')" alt="URL Control Options" style="float: right;">

该控件在继承 `Control_Base_Multiple` 类的 `Control_URL` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::URL` 常量。

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
			<td>url</td>
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
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>placeholder</code></td>
			<td><code>string</code></td>
			<td>Paste URL or type</td>
			<td>当字段没有值时显示的占位符。</td>
		</tr>
		<tr>
			<td><code>autocomplete</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>是否允许搜索功能。</td>
		</tr>
		<tr>
			<td><code>options</code></td>
			<td><code>array</code>|<code>false</code></td>
			<td>[<br>'url',<br>'is_external',<br>'nofollow',<br>'custom_attributes'<br>]</td>
			<td>要显示的 URL 选项数组。默认显示所有选项。但您可以选择显示哪些 URL 元素。将选项设置为 <code>false</code> 将禁用所有选项。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				字段的默认值。
				<ul>
					<li><strong>$url</strong> (<code>string</code>) URL。</li>
					<li><strong>$is_external</strong> (<code>bool</code>) 是在同一标签页还是新标签页中打开 URL。</li>
					<li><strong>$nofollow</strong> (<code>bool</code>) 是否添加 nofollow 属性。</li>
					<li><strong>$custom_attributes</strong> (<code>string</code>) 自定义属性字符串，以逗号分隔的 key|value 对字符串形式提供。</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## 返回值

```
[
	'url' => 'https://your-link.com',
	'is_external' => true,
	'nofollow' => true,
	'custom_attributes' => '',
]
```

(_`array`_) 包含链接数据的数组：

*   **$url** (_`string`_) URL 地址。
*   **$is_external** (_`bool`_) 是否在新标签页中打开链接。
*   **$nofollow** (_`bool`_) 是否添加 nofollow 属性。
*   **$custom_attributes** (_`string`_) 自定义属性字符串，格式为逗号分隔的 `key|value` 键值对。

## Usage

```php {14-28,36-38,40-42,48-50}
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
			'website_link',
			[
				'label' => esc_html__( 'Link', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::URL,
				'options' => [ 'url', 'is_external', 'nofollow' ],
				'default' => [
					'url' => '',
					'is_external' => true,
					'nofollow' => true,
					// 'custom_attributes' => '',
				],
				'label_block' => true,
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		if ( ! empty( $settings['website_link']['url'] ) ) {
			$this->add_link_attributes( 'website_link', $settings['website_link'] );
		}
		?>
		<a <?php $this->print_render_attribute_string( 'website_link' ); ?>>
			...
		</a>
		<?php
	}

	protected function content_template(): void {
		?>
		<a href="{{ settings.website_link.url }}">
			...
		</a>
		<?php
	}

}
```
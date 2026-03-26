---
title: "画廊控件"
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

# 画廊控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-gallery.png')" alt="Gallery Control" style="float: right;">

Elementor 画廊控件基于 WordPress 画廊显示一个媒体选择区域。该控件允许从 WordPress 媒体库中选择多张图片。

该控件在继承 `Base_Data_Control` 类的 `Control_Gallery` 类中定义。

<img :src="$withBase('/assets/img/controls/control-gallery2.png')" alt="Gallery Control" style="float: right;">

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::GALLERY` 常量。

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
			<td>gallery</td>
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
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>默认图库图片。包含图片 ID 和 URL 的图片数组。</td>
		</tr>
	</tbody>
</table>

## 返回值

```
[
	[
		'id' => 0,
		'url' => ''
	],
	[
		'id' => 0,
		'url' => ''
	],
]
```

(_`array`_) 一个由单个图片数组组成的数组，包含每个图片的 ID 和 URL：

* **$id** (_`int`_) 媒体 ID。
* **$url** (_`string`_) 媒体 URL。

## Usage

```php {14-22,30-32,37-39}
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
			'gallery',
			[
				'label' => esc_html__( 'Add Images', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::GALLERY,
				'show_label' => false,
				'default' => [],
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		foreach ( $settings['gallery'] as $image ) {
			echo '<img src="' . esc_attr( $image['url'] ) . '">';
		}
	}

	protected function content_template(): void {
		?>
		<# _.each( settings.gallery, function( image ) { #>
			<img src="{{ image.url }}">
		<# }); #>
		<?php
	}

}
```
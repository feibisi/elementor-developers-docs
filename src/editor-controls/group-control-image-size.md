---
title: "图像尺寸组控件"
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

# 图像尺寸组控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 图像尺寸组控件显示输入字段，用于定义默认图像尺寸（缩略图、中等、中等大、大）或自定义图像尺寸。

该控件在 `Group_Control_Image_Size` 类中定义，该类继承自 `Group_Control_Base` 类。

使用此组控件时，`type` 应设置为 `Group_Control_Image_Size::get_type()` 方法。

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
			<td>image-size</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>include</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>要包含的图像尺寸。</td>
		</tr>
		<tr>
			<td><code>exclude</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>要排除的图像尺寸。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>默认的图像尺寸。</td>
		</tr>
	</tbody>
</table>

## 返回值

```
[
	'{name}_size' => '',
	'{name}_custom_dimension' => '',
]
```

(_`array`_) 包含图像尺寸值的数组。

* **${name}_size** (_`string`_) 图像尺寸。
* **${name}_custom_dimension** (_`string`_) 图像维度。

## Usage

```php {14-33,41,46-56}
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
			'image',
			[
				'label' => esc_html__( 'Choose Image', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::MEDIA,
				'default' => [
					'url' => \Elementor\Utils::get_placeholder_image_src(),
				],
			]
		);

		$this->add_group_control(
			\Elementor\Group_Control_Image_Size::get_type(),
			[
				'name' => 'thumbnail', // Usage: `{name}_size` and `{name}_custom_dimension`, in this case `thumbnail_size` and `thumbnail_custom_dimension`.
				'exclude' => [ 'custom' ],
				'include' => [],
				'default' => 'large',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		echo \Elementor\Group_Control_Image_Size::get_attachment_image_html( $settings, 'thumbnail', 'image' );
	}

	protected function content_template(): void {
		?>
		<#
		const image = {
			id: settings.image.id,
			url: settings.image.url,
			size: settings.thumbnail_size,
			dimension: settings.thumbnail_custom_dimension,
			model: view.getEditModel()
		};
		const image_url = elementor.imagesManager.getImageUrl( image );
		#>
		<img src="{{{ image_url }}}" />
		<?php
	}

}
```
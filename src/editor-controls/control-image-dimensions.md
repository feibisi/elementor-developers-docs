---
title: "Image Dimensions Control"
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

# Image Dimensions Control

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-image-dimensions.png')" alt="Image Dimensions Control" style="float: right;">

Elementor image dimensions control displays a width input, a height input and an apply button. It is used by the [Image Size group control](src/editor-controls/group-control-image-size) to allow the user to set custom width or height for an image.

The control is defined in `Control_Image_Dimensions` class which extends `Control_Base_Multiple` class.

When using this control, the `type` should be set to `\Elementor\Controls_Manager::IMAGE_DIMENSIONS` constant.

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
			<td>image_dimensions</td>
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
			<td>false</td>
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
			<td>
				默认的图像尺寸值。
				<ul>
					<li><strong>$width</strong> (<code>int</code>) 图像宽度。</li>
					<li><strong>$height</strong> (<code>int</code>) 图像高度。</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## 返回值

```
[
	'width' => '',
	'height' => '',
]
```

(_`array`_) 一个包含图像尺寸值的数组：

*   **$width** (_`int`_) 图像宽度。
*   **$height** (_`int`_) 图像高度。

## 用法

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
			'custom_dimension',
			[
				'label' => esc_html__( 'Image Dimension', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::IMAGE_DIMENSIONS,
				'description' => esc_html__( 'Crop the original image size to any custom size. Set custom width or height to keep the original size ratio.', 'textdomain' ),
				'default' => [
					'width' => '',
					'height' => '',
				],
			]
		);

		$this->end_controls_section();

	}

}
```
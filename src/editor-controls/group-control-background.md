---
title: "背景组控件"
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

# 背景组控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 背景组控件显示用于定义背景的输入字段，包括背景颜色、背景图像、背景渐变或背景视频。

该控件在继承 `Group_Control_Base` 类的 `Group_Control_Background` 类中定义。

使用此组控件时，`type` 应设置为 `Group_Control_Background::get_type()` 方法。

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
			<td>background</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>types</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>要使用的特定背景类型。可用类型包括 <code>classic</code>、<code>gradient</code>、<code>video</code> 和 <code>slideshow</code>。默认为空数组，包含所有类型。</td>
		</tr>
		<tr>
			<td><code>include</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>从组控件中包含特定的控件。示例：<code>['image']</code></td>
		</tr>
		<tr>
			<td><code>exclude</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>从组控件中排除某些控件。示例：<code>['image']</code></td>
		</tr>
		<tr>
			<td><code>fields_options</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>一个多维数组，包含覆盖控件设置的数据。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`array`_) An array containing the background values.

## Usage

```php {14-21,30-32,38-40}
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

		$this->add_group_control(
			\Elementor\Group_Control_Background::get_type(),
			[
				'name' => 'background',
				'types' => [ 'classic', 'gradient', 'video' ],
				'selector' => '{{WRAPPER}} .your-class',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		?>
		<div class="your-class">
			...
		</div>
		<?php
	}

	protected function content_template(): void {
		?>
		<div class="your-class">
			...
		</div>
		<?php
	}

}
```

## 注意事项

视频和幻灯片类型仅支持在分区/容器级别使用，不支持在小部件级别使用。
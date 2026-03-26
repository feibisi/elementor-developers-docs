---
title: "Hover Animation Control"
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

# Hover Animation Control

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-hover-animation.png')" alt="Hover Animation Control" style="float: right;">

Elementor hover animation control displays a select box field based on the [Hover.css](https://ianlunn.github.io/Hover/) library. The control allows to set an hover animation effect for an item.

The control is defined in `Control_Hover_Animation` class which extends `Base_Data_Control` class.

When using this control, the `type` should be set to `\Elementor\Controls_Manager::HOVER_ANIMATION` constant.

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
			<td>hover_animation</td>
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
			<td><code>string</code></td>
			<td></td>
			<td>字段的默认值。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`_) The selected hover animation class.

## Usage

```php {14-20,29-33,35-37,43-52}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_control(
			'hover_animation',
			[
				'label' => esc_html__( 'Hover Animation', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::HOVER_ANIMATION,
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		$elementClass = 'container';

		if ( $settings['hover_animation'] ) {
			$elementClass .= ' elementor-animation-' . $settings['hover_animation'];
		}

		$this->add_render_attribute( 'wrapper', 'class', $elementClass );
		?>
		<div <?php $this->print_render_attribute_string( 'wrapper' ); ?>>
			...
		</div>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		const elementClass = 'container';

		if ( '' !== settings.hover_animation ) {
			elementClass += ' elementor-animation-' + settings.hover_animation;
		}

		view.addRenderAttribute( 'wrapper', { 'class': elementClass } );
		#>
		<div {{{ view.getRenderAttributeString( 'wrapper' ) }}}>
			...
		</div>
		<?php
	}

}
```
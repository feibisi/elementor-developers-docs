---
title: "退出动画控制"
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

# 退出动画控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-exit-animation.png')" alt="Exit Animation Control" style="float: right;">

Elementor 退出动画控制基于 [Animate.css](https://animate.style/) 库显示一个选择框字段。该控制允许为项目设置退出动画效果。

该控件在 `Control_Exit_Animation` 类中定义，该类继承自 `Control_Animation` 类，而 `Control_Animation` 类又继承自 `Base_Data_Control` 类。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::EXIT_ANIMATION` 常量。

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
			<td>exit_animation</td>
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
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>字段的默认值。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`_) The selected exit animation class.

## Usage

```php {14-21,30-32,38-40}
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
			'exit_animation',
			[
				'label' => esc_html__( 'Exit Animation', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::EXIT_ANIMATION,
				'prefix_class' => 'animated ',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		?>
		<div class="<?php echo esc_attr( $settings['exit_animation'] ); ?>">
			...
		</div>
		<?php
	}

	protected function content_template(): void {
		?>
		<div class="{{ settings.exit_animation }}">
			...
		</div>
		<?php
	}

}
```
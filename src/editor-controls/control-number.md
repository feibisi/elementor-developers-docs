---
title: "数值控制"
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

# 数值控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-number.png')" alt="Number Control" style="float: right;">

Elementor 数值控件显示一个简单的数字输入字段，可选择限制最小值和最大值，并定义数值变化时的步长。

该控件在继承 `Base_Data_Control` 类的 `Control_Number` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::NUMBER` 常量。

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
			<td>number</td>
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
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>min</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>最小值（仅影响微调器，用户仍可输入更低的值）。</td>
		</tr>
		<tr>
			<td><code>max</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>最大值（仅影响微调器，用户仍可输入更高的值）。</td>
		</tr>
		<tr>
			<td><code>step</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>使用控件微调器时递增或递减的间隔值。默认为空，值将递增 1。</td>
		</tr>
		<tr>
			<td><code>placeholder</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>字段无值时显示的占位符。</td>
		</tr>
		<tr>
			<td><code>title</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>鼠标悬停时显示的字段标题。</td>
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

(_`string`_) The number field value.

## Usage

```php {14-24,37-39,50-52}
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
			'price',
			[
				'label' => esc_html__( 'Price', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::NUMBER,
				'min' => 5,
				'max' => 100,
				'step' => 5,
				'default' => 10,
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['price'] ) ) {
			return;
		}
		?>
		<span class="price">
			<?php echo $settings['price']; ?>
		</span>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.price ) {
			return;
		}
		#>
		<span class="price">
			{{{ settings.price }}}
		</span>
		<?php
	}

}
```
---
title: "开关控件"
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

# 开关控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-switcher.png')" alt="Switcher Control" style="float: right;">

Elementor 开关控件显示一个开/关切换器。它本质上是复选框的一种精美表现形式。

<img :src="$withBase('/assets/img/controls/control-switcher-checked.png')" alt="Checked Switcher Control" style="float: right;">

该控件定义在继承 `Base_Data_Control` 类的 `Control_Switcher` 类中。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::SWITCHER` 常量。

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
			<td>switcher</td>
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
			<td><code>label_on</code></td>
			<td><code>string</code></td>
			<td>Yes</td>
			<td>“未选中”状态的标签。</td>
		</tr>
		<tr>
			<td><code>label_off</code></td>
			<td><code>string</code></td>
			<td>No</td>
			<td>“已选中”状态的标签。</td>
		</tr>
		<tr>
			<td><code>return_value</code></td>
			<td><code>string</code></td>
			<td>yes</td>
			<td>选中时返回的值。</td>
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

(_`string`_) The switcher field value, based on `return_value` argument.

## Usage

```php {14-24,41-43,48-50}
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
			'show_title',
			[
				'label' => esc_html__( 'Show Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::SWITCHER,
				'label_on' => esc_html__( 'Show', 'textdomain' ),
				'label_off' => esc_html__( 'Hide', 'textdomain' ),
				'return_value' => 'yes',
				'default' => 'yes',
			]
		);

		$this->add_control(
			'title',
			[
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'default' => esc_html__( 'Default title', 'textdomain' ),
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		if ( 'yes' === $settings['show_title'] ) {
			echo '<h2>' . $settings['title'] . '</h2>';
		}
	}

	protected function content_template(): void {
		?>
		<# if ( 'yes' === settings.show_title ) { #>
			<h2>{{{ settings.title }}}</h2>
		<# } #>
		<?php
	}

}
```
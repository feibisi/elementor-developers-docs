---
title: "日期时间控件"
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

# 日期时间控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-date-time.png')" alt="Date Time Control" style="float: right;">

Elementor 日期时间控件基于 [Flatpickr](https://flatpickr.js.org/) 库显示一个日期/时间选择器字段。

该控件定义在继承 `Base_Data_Control` 类的 `Control_Date_Time` 类中。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::DATE_TIME` 常量。

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
			<td>date_time</td>
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
			<td><code>picker_options</code></td>
			<td><code>array</code></td>
			<td>enableTime:true,<br>
				minuteIncrement:1
			</td>
			<td>选择器的<a href="https://chmln.github.io/flatpickr/options/" target="_blank" rel="noopener">配置</a>。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>默认日期/时间，使用 MySQL 格式 (<code>YYYY-mm-dd HH:ii</code>)。</td>
		</tr>
	</tbody>
</table>

## Return Value

(_`string`_) The chosen date/time in MySQL format (`YYYY-mm-dd HH:ii`).

## Usage

```php {14-20,32-33,35,41-46}
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
			'due_date',
			[
				'label' => esc_html__( 'Due Date', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::DATE_TIME,
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['due_date'] ) ) {
			return;
		}

		$due_date = strtotime( $settings['due_date'] );
		$due_date_in_days = $due_date / DAY_IN_SECONDS;
		?>
		<p><?php printf( esc_html__( 'Something will happen in %s days.', 'textdomain' ), $due_date_in_days ); ?></p>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.due_date ) {
			return;
		}

		const due_date = new Date( settings.due_date );
		const now_date = new Date();
		const due_date_in_days = Math.floor( ( due_date - now_date ) / 86400000 ); // 86400000 milliseconds in one Day.
		#>
		<p> Something will happen in {{{ due_date_in_days }}} days. </p>
		<?php
	}

}
```
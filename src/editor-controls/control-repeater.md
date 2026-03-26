---
title: "重复器控件"
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

# 重复器控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

<img :src="$withBase('/assets/img/controls/control-repeater.png')" alt="Repeater Control" style="float: right;">

Elementor 重复器控件允许您构建可重复的字段块。例如，您可以创建一组包含标题和 WYSIWYG 文本的字段——用户随后将能够添加“行”，每行都包含一个标题和一段文本。这些数据可以包装在自定义 HTML 标签中，使用 CSS 进行设计，并通过 JS 或外部库实现交互。

该控件在继承 `Base_Data_Control` 类的 `Control_Repeater` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::REPEATER` 常量。

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
			<td>repeater</td>
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
			<td><code>fields</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>一个包含重复器字段的多维数组。</td>
		</tr>
		<tr>
			<td><code>title_field</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>当项目被最小化时，将在字段列表中用作重复器标题的字段。</td>
		</tr>
		<tr>
			<td><code>prevent_empty</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>是否防止删除第一个重复器字段。以保持至少一个重复器字段。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>默认的重复器值。一个多维数组，包含字段作为键，每个键的默认值作为值：<code>[ [ 'title' =&gt; '', 'content' =&gt; '' ], [ 'title' =&gt; '', 'content' =&gt; '' ], ... ]</code></td>
		</tr>
	</tbody>
</table>

## Return Value

(_`array`_) A multi dimensional array containing inner fields values.

## Usage

Usage example with `fields` array:

```php {14-55,64-71,76-83}
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
			'list',
			[
				'label' => esc_html__( 'Repeater List', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::REPEATER,
				'fields' => [
					[
						'name' => 'list_title',
						'label' => esc_html__( 'Title', 'textdomain' ),
						'type' => \Elementor\Controls_Manager::TEXT,
						'default' => esc_html__( 'List Title' , 'textdomain' ),
						'label_block' => true,
					],
					[
						'name' => 'list_content',
						'label' => esc_html__( 'Content', 'textdomain' ),
						'type' => \Elementor\Controls_Manager::WYSIWYG,
						'default' => esc_html__( 'List Content' , 'textdomain' ),
						'show_label' => false,
					],
					[
						'name' => 'list_color',
						'label' => esc_html__( 'Color', 'textdomain' ),
						'type' => \Elementor\Controls_Manager::COLOR,
						'selectors' => [
							'{{WRAPPER}} {{CURRENT_ITEM}}' => 'color: {{VALUE}}'
						],
					]
				],
				'default' => [
					[
						'list_title' => esc_html__( 'Title #1', 'textdomain' ),
						'list_content' => esc_html__( 'Item content. Click the edit button to change this text.', 'textdomain' ),
					],
					[
						'list_title' => esc_html__( 'Title #2', 'textdomain' ),
						'list_content' => esc_html__( 'Item content. Click the edit button to change this text.', 'textdomain' ),
					],
				],
				'title_field' => '{{{ list_title }}}',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( $settings['list'] ) {
			echo '<dl>';
			foreach (  $settings['list'] as $item ) {
				echo '<dt class="elementor-repeater-item-' . esc_attr( $item['_id'] ) . '">' . $item['list_title'] . '</dt>';
				echo '<dd>' . $item['list_content'] . '</dd>';
			}
			echo '</dl>';
		}
	}

	protected function content_template(): void {
		?>
		<# if ( settings.list.length ) { #>
			<dl>
			<# _.each( settings.list, function( item ) { #>
				<dt class="elementor-repeater-item-{{ item._id }}">{{{ item.list_title }}}</dt>
				<dd>{{{ item.list_content }}}</dd>
			<# }); #>
			</dl>
		<# } #>
		<?php
	}

}
```

Usage example with `Repeater()` class:

```php {14-45,52,74-81,86-93}
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

		$repeater = new \Elementor\Repeater();

$repeater->add_control(
			'list_title',
			[
				'label' => esc_html__( '标题', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'default' => esc_html__( '列表标题' , 'textdomain' ),
				'label_block' => true,
			]
		);

		$repeater->add_control(
			'list_content',
			[
				'label' => esc_html__( '内容', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::WYSIWYG,
				'default' => esc_html__( '列表内容' , 'textdomain' ),
				'show_label' => false,
			]
		);

		$repeater->add_control(
			'list_color',
			[
				'label' => esc_html__( '颜色', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::COLOR,
				'selectors' => [
					'{{WRAPPER}} {{CURRENT_ITEM}}' => 'color: {{VALUE}}'
				],
			]
		);

		$this->add_control(
			'list',
			[
				'label' => esc_html__( '重复列表', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::REPEATER,
				'fields' => $repeater->get_controls(),
				'default' => [
					[
						'list_title' => esc_html__( '标题 #1', 'textdomain' ),
						'list_content' => esc_html__( '项目内容。点击编辑按钮修改此文本。', 'textdomain' ),
					],
					[
						'list_title' => esc_html__( '标题 #2', 'textdomain' ),
						'list_content' => esc_html__( '项目内容。点击编辑按钮修改此文本。', 'textdomain' ),
					],
				],
				'title_field' => '{{{ list_title }}}',
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( $settings['list'] ) {
			echo '<dl>';
			foreach (  $settings['list'] as $item ) {
				echo '<dt class="elementor-repeater-item-' . esc_attr( $item['_id'] ) . '">' . $item['list_title'] . '</dt>';
				echo '<dd>' . $item['list_content'] . '</dd>';
			}
			echo '</dl>';
		}
	}

	protected function content_template(): void {
		?>
		<# if ( settings.list.length ) { #>
			<dl>
			<# _.each( settings.list, function( item ) { #>
				<dt class="elementor-repeater-item-{{ item._id }}">{{{ item.list_title }}}</dt>
				<dd>{{{ item.list_content }}}</dd>
			<# }); #>
			</dl>
		<# } #>
		<?php
	}

}
```

## 注意事项

中继器可以[有条件地显示](src/editor-controls/conditional-display#repeaters-conditional-display)。但必须明确了解有条件显示中继器字段时，哪些操作可行，哪些不可行。
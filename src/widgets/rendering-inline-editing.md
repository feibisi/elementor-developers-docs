---
title: "Rendering Inline Editing"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Widgets
    - Src
    - Repos
---

# Rendering Inline Editing

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

When developing widgets, developers can define which controls will be inline editable in both the editor panel and preview area.

<iframe width="560" height="315"src="https://www.youtube.com/embed/miNu2oONgYI" frameborder="0" allowfullscreen></iframe>

## Inline Editing Toolbars

Elementor supports the following types of toolbars for inline editing:

* **No Toolbar** – `(none)` Inline text editing without a toolbar, just typing text inline.
* **Basic Toolbar** – `(basic)` Inline text editing with a minimal toolbar, including: bold, italic and underline buttons.
* **Advanced Toolbar** – `(advanced)` Inline text editing with a full toolbar, including: adding/removing links, H1-H6 heading, blockquote, preformatting and bulleted or numbered list buttons.

<img :src="$withBase('/assets/img/inline-editing-example.png')" alt="Inline editing example">

Elementor recommends using inline editing as follows:

* **Input controls** – use inline editing without any toolbars in simple text/number/url/email fields.
* **Textarea controls** – use inline editing with a minimal toolbar.
* **Wysiwyg controls** – use inline editing with a full toolbar.

## 添加内联编辑功能

内联编辑支持通过在 widget 的 `render()` 方法中使用 `add_inline_editing_attributes()` 方法，以及在 `content_template()` 中使用 `addInlineEditingAttributes()` 方法来添加。

每个内联编辑属性包含两个参数：

*   **键** `(string)` – 代码中使用的唯一名称。
*   **工具栏** `(string)` – 工具栏类型。可接受的值有：`advanced`、`basic` 或 `none`。默认值为 `none`。

使用以下方式添加新的内联编辑属性：

```php {5-6,11-12}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function render(): void {
		$this->add_inline_editing_attributes( 'text', 'advanced' );
		echo '<div ' . $this->get_render_attribute_string( 'text' ) . '>' . $this->get_settings( 'text' ) . '</div>';
	}

	protected function content_template(): void {
		?>
		<# view.addInlineEditingAttributes( 'text', 'advanced' ); #>
		<div {{{ view.getRenderAttributeString( 'text' ) }}}>{{{ settings.text }}}</div>
		<?php
	}

}
```

## Example of Inline Editing

The following is a full example using three controls all having inline support. This includes simple text without a toolbar, a textarea with a basic toolbar, and a wysiwyg with an advanced toolbar:

```php {48-50,52-54,61-63,65-67}
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
			'title',
			[
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'default' => esc_html__( 'Title', 'textdomain' ),
			]
		);

		$this->add_control(
			'description',
			[
				'label' => esc_html__( 'Description', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXTAREA,
				'default' => esc_html__( 'Description', 'textdomain' ),
			]
		);

		$this->add_control(
			'content',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::WYSIWYG,
				'default' => esc_html__( 'Content', 'textdomain' ),
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		$this->add_inline_editing_attributes( 'title', 'none' );
		$this->add_inline_editing_attributes( 'description', 'basic' );
		$this->add_inline_editing_attributes( 'content', 'advanced' );
		?>
		<h2 <?php $this->print_render_attribute_string( 'title' ); ?>><?php echo $settings['title']; ?></h2>
		<div <?php $this->print_render_attribute_string( 'description' ); ?>><?php echo $settings['description']; ?></div>
		<div <?php $this->print_render_attribute_string( 'content' ); ?>><?php echo $settings['content']; ?></div>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		view.addInlineEditingAttributes( 'title', 'none' );
		view.addInlineEditingAttributes( 'description', 'basic' );
		view.addInlineEditingAttributes( 'content', 'advanced' );
		#>
		<h2 {{{ view.getRenderAttributeString( 'title' ) }}}>{{{ settings.title }}}</h2>
		<div {{{ view.getRenderAttributeString( 'description' ) }}}>{{{ settings.description }}}</div>
		<div {{{ view.getRenderAttributeString( 'content' ) }}}>{{{ settings.content }}}</div>
		<?php
	}

}
```
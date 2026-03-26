---
title: "字段内容模板"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Form Fields
    - Src
    - Repos
---

# 字段内容模板

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

在[渲染小部件](src/widgets/widget-rendering)时，我们有一个 PHP 模板和一个 JS 模板。然而，[表单字段渲染](src/form-fields/field-render)只有 PHP 模板，没有 JS 模板。外部开发者可以使用一种变通方法来克服这个障碍。

## 渲染 JS 模板

以下代码是一个简单的变通方法，用于在 Elementor 编辑器中渲染 JS 模板。

```php
<?php
class Elementor_Test_Field extends \ElementorPro\Modules\Forms\Fields\Field_Base {

	public function __construct() {
		parent::__construct();
		add_action( 'elementor/preview/init', [ $this, 'editor_preview_footer' ] );
	}

	public function editor_preview_footer(): void {
		add_action( 'wp_footer', [ $this, 'content_template_script' ] );
	}

	public function content_template_script(): void {
		?>
		<script>
		jQuery( document ).ready( () => {

			elementor.hooks.addFilter(
				'elementor_pro/forms/content_template/field/<?php echo $this->get_type(); ?>',
				function ( inputField, item, i ) {
					const fieldType  = 'text';
					const fieldId    = `form_field_${i}`;
					const fieldClass = `elementor-field-textual elementor-field ${item.css_classes}`;
					const title      = "<?php echo esc_html__( 'Some text...', 'textdomain' ); ?>";

					return `<input type="${fieldType}" id="${fieldId}" class="${fieldClass}" title="${title}">`;
				}, 10, 3
			);

		});
		</script>
		<?php
	}

}
```

::: warning 请注意
1. 上述描述的变通方法是一个临时解决方案。
2. 我们可能会引入一个官方的 `content_template()` 方法来渲染 JS 模板，就像为 Elementor 小部件所做的那样。
3. 为确保您的代码具有未来兼容性，请确保您的字段类没有名为 `content_template()` 的方法。
:::
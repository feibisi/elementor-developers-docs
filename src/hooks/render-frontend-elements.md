---
title: "Render Frontend Elements"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Hooks
    - Src
    - Repos
---

# Render Frontend Elements

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor has a hook that lets developers add code before or after elements in the frontend. This hook can be applied to either a single element or all the elements on a page and is applied to the final HTML output of the element(s).  Developers can use this hook to change the HTML output before Elementor displays it to the end-user.

## 钩子详情

* **钩子类型：** 动作钩子
* **钩子名称：**
  * `elementor/frontend/before_render`
  * `elementor/frontend/after_render`
  * `elementor/frontend/{$element_type}/before_render`
  * `elementor/frontend/{$element_type}/after_render`
* **说明：** 钩子名称中的动态部分 `$element_type` 指的是 `元素类型`。
* **影响范围：** 前端

## Hook Arguments

| Argument  | Type                        | Description           |
|-----------|-----------------------------|-----------------------|
| `element` | _`\Elementor\Element_Base`_ | The element instance. |

## 元素类型

动态部分 `$element_type` 指的是您要定位的元素类型。例如，以下是一些可用的元素类型：

* `section` - 应用于版块和内部版块。
* `column` - 应用于列和内部列。
* `container` - 应用于容器和内部容器。
* `widget` - 应用于所有小部件。

## Example

### All Elements

Apply changes to all the elements:

```php
<?php
/**
 * Add `<div>` before all the elements in the page.
 *
 * @since 1.0.0
 * @param \Elementor\Element_Base $element The element instance.
 */
function add_div_before_all_elements( $element ) {
	?>
	<div class="before-element">Text before element</div>
	<?php
}
add_action( 'elementor/frontend/before_render', 'add_div_before_all_elements' );

/**
 * Add `<div>` after all the elements in the page.
 *
 * @since 1.0.0
 * @param \Elementor\Element_Base $element The element instance.
 */
function add_div_after_all_elements( $element ) {
	?>
	<div class="after-element">Text after element</div>
	<?php
}
add_action( 'elementor/frontend/after_render', 'add_div_after_all_elements' );
```

### Specific Elements

Apply changes only on widgets:

```php
<?php
/**
 * Add `<div>` before all the widgets in the page.
 *
 * @since 1.0.0
 * @param \Elementor\Element_Base $element The element instance.
 */
function add_div_before_all_the_widget( $element ) {
	?>
	<div class="before-widget">Text before widget</div>
	<?php
}
add_action( 'elementor/frontend/widget/before_render', 'add_div_before_all_the_widget' );

/**
 * Add `<div>` after all the widgets in the page.
 *
 * @since 1.0.0
 * @param \Elementor\Element_Base $element The element instance.
 */
function add_div_after_all_the_widget( $element ) {
	?>
	<div class="after-widget">Text after widget</div>
	<?php
}
add_action( 'elementor/frontend/widget/after_render', 'add_div_after_all_the_widget' );
```

### Advanced Usage

Change the element instance using the `$element` parameter.

```php
<?php
/**
 * Add a custom class and a data attribute to all the elements
 * containing a specific setting defined through the element control.
 *
 * @since 1.0.0
 * @param \Elementor\Element_Base $element The element instance.
 */
function add_attributes_to_elements( $element ) {

	if ( ! $element->get_settings( 'my-custom-setting' ) ) {
		return;
	}

	$element->add_render_attribute(
		'_wrapper',
		[
			'class' => 'my-custom-class',
			'data-my-custom-value' => 'my-custom-data-value',
		]
	);

}
add_action( 'elementor/frontend/before_render', 'add_attributes_to_elements' );
```
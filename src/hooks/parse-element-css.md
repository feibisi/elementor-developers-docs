---
title: "解析元素 CSS"
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

# 解析元素 CSS

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 提供了一个钩子，允许开发者在 CSS 文件生成之前向元素添加新的 CSS 规则。

## 钩子详情

* **钩子类型:** 动作钩子
* **钩子名称:** `elementor/element/parse_css`
* **影响范围:** 前端

## 钩子参数

| 参数        | 类型                                   | 描述                     |
|-------------|----------------------------------------|--------------------------|
| `post_css`  | _`\Elementor\Core\Files\CSS\Post`_     | 文章 CSS 文件实例        |
| `element`   | _`\Elementor\Element_Base`_            | 元素实例                 |

## 示例

让我们向生成的 CSS 文件添加一个简单的 CSS 规则：

```php
/**
 * 添加自定义 CSS 规则。
 *
 * @since 1.0.0
 * @param \Elementor\Core\Files\CSS\Post $post_css_file 文章 CSS 文件实例。
 * @param \Elementor\Element_Base        $element       元素实例。
 */
function add_custom_css_rule_to_the_css_file( $post_css_file, $element ) {

	$post_css_file->get_stylesheet()->add_rules(
		'.my-selector',
		[
			'width' => '50px',
			'height' => '50px',
		]
	);

}
add_action(	'elementor/element/parse_css', 'add_custom_css_rule_to_the_css_file', 10, 2 );
```

现在，让我们添加一个带有唯一 Elementor 选择器的 CSS 规则：

```php
/**
 * 解析元素 CSS。
 *
 * @since 1.0.0
 * @param \Elementor\Core\Files\CSS\Post $post_css_file 文章 CSS 文件实例。
 * @param \Elementor\Element_Base        $element       元素实例。
 */
function add_custom_rules_to_css_file( $post_css_file, $element ) {

	$item_width = some_get_theme_config_function( 'item_width' );
	$item_height = some_get_theme_config_function( 'item_height' );

	$post_css_file->get_stylesheet()->add_rules(
		$element->get_unique_selector(),
		[
			'width' => $item_width . 'px',
			'height' => $item_height . 'px',
		]
	);

}
add_action(	'elementor/element/parse_css', 'add_custom_rules_to_css_file', 10, 2 );
```
---
title: "小部件分类"
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

# 小部件分类

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor **小部件分类** 用于将小部件组织成组。当 Elementor 初始化时，它会注册几个默认分类。只有当分类被分配了小部件时，它们才会显示在小部件面板中。

## 使用小部件分类

我们在注册新的 Elementor 小部件时会使用小部件分类。通过扩展 `\Elementor\Widget_Base` 类，我们继承了 `\Elementor\Widget_Base::get_categories()` 方法，该方法默认返回通用分类。要将小部件分配到不同的分类，我们需要重写该方法并按以下方式返回新的分类：

```php {3-5}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function get_categories(): array {
		return [ 'basic' ];
	}

}
```

## 默认分类

当您选择将小部件分配到哪个分类时，可以从以下默认分类中选择一个：

* **Basic** – `basic` 分类。
* **Pro** – Elementor Pro 的 `pro-elements` 分类。
* **Theme** – Elementor Pro 的 `theme-elements` 分类。
* **WooCommerce** – Elementor Pro 的 `woocommerce-elements` 分类。
* **General** – `general` 分类。
* **WordPress** – 显示 WordPress 小部件的 `wordpress` 分类。

或者，您可以注册自己的分类。

## 创建新分类

Elementor 允许开发者添加新的小部件分类来分组他们自己的自定义小部件。注册新的小部件分类需要使用 `elementor/elements/categories_registered` 动作。

请注意，创建新分类时，您需要提供分类名称/别名、分类标题/标签和分类图标。

```php
function add_elementor_widget_categories( $elements_manager ) {

	$elements_manager->add_category(
		'first-category',
		[
			'title' => esc_html__( 'First Category', 'textdomain' ),
			'icon' => 'fa fa-plug',
		]
	);
	$elements_manager->add_category(
		'second-category',
		[
			'title' => esc_html__( 'Second Category', 'textdomain' ),
			'icon' => 'fa fa-plug',
		]
	);

}
add_action( 'elementor/elements/categories_registered', 'add_elementor_widget_categories' );
```
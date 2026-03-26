---
title: "小部件分类"
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

# 小部件分类

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

<img :src="$withBase('/assets/img/elementor-categories.png')" alt="Elementor Widget Categories" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

Elementor 的**小部件分类**用于将小部件分组管理。Elementor 初始化时，会注册多个默认分类。

只有当分类下分配有小部件时，该分类才会在部件面板中显示。

外部开发者可以创建新的分类，并在品牌专属的分类中单独展示他们的小部件。

## 使用小部件分类

在注册新的 Elementor 小部件时，我们会使用小部件分类。通过继承 `\Elementor\Widget_Base` 类，我们同时也继承了 `\Elementor\Widget_Base::get_categories()` 方法，该方法默认返回 `general` 分类。

要将小部件分配到不同的分类，我们需要重写此方法，并按以下方式返回新的分类：

```php {3-5}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function get_categories(): array {
		return [ 'basic' ];
	}

}
```

## Default Categories

When you select which category to assign your widget to, you can select one of the default categories:

| Label           | Name                   | Package      | Description                                     |
|-----------------| ---------------------- | ------------ | ----------------------------------------------- |
| **Basic**       | `basic`                | Elementor    | Category for basic widgets                      |
| **Pro**         | `pro-elements`         | ElementorPro | Category for advanced widgets                   |
| **General**     | `general`              | Elementor    | Category for general widgets                    |
| **Site**        | `theme-elements`       | ElementorPro | Category for site & theme widgets               |
| **WooCommerce** | `woocommerce-elements` | ElementorPro | Category for WooCommerce widgets                |
| **{Custom}**    |                        | {Addons}     | Custom categories added by external developers  |
| **WordPress**   | `wordpress`            | WordPress    | Category for WordPress widgets                  |

Or you can register your own category.

## 创建新分类

Elementor 允许开发者添加新的小部件分类，用于分组自定义小部件。注册新分类需使用 `elementor/elements/categories_registered` 动作。

注意：创建新分类时，需要提供分类名称/别名、分类标题/标签以及分类图标。

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
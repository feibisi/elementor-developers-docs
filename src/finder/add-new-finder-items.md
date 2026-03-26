---
title: "添加新的查找器项目"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Finder
    - Src
    - Repos
---

# 添加新的查找器项目

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

对于添加到查找器的每个新项目（链接），我们需要定义几个字段。这包括标签、URL、图标等。所有这些链接被分组在一个数组中并一起返回。

## 新建类别

查找器类别包含所有类别标签及其项目。

```php
class New_Finder_Category extends \Elementor\Core\Common\Modules\Finder\Base_Category {

	public function get_id(): string {
		return 'my-category-name';
	}

	public function get_title(): string {
		return esc_html__( 'Category Label', 'textdomain' );
	}

	public function get_category_items( array $options = [] ): array {
		return [
			'elementor-website' => [
				'title' => esc_html__( 'Elementor', 'textdomain' ),
				'icon' => 'elementor',
				'url' => 'https://elementor.com/',
				'keywords' => [ 'elementor', 'website' ],
			],
			'wordpress-website' => [
				'title' => esc_html__( 'WordPress', 'textdomain' ),
				'icon' => 'wordpress',
				'url' => 'https://wordpress.org/',
				'keywords' => [ 'wordpress', 'website' ],
			],
		];
	}

}
```

每个项目必须包含以下属性：

  * **name** – 用于定义 `$items` 数组中的 ID（必需）。
  * **title** – 用于定义向用户显示的标签（必需）。
  * **icon** – 用于定义在标题/标签前显示的图标。
  * **url** – 用于定义 URL（必需）。
  * **keywords** – 用于定义相关的搜索关键词。

## 注册查找器类别

当查找器类别类准备就绪后，我们必须将其添加到类别管理器中。这是通过 `elementor/finder/register` 动作钩子完成的。

添加新类别时，我们需要提供类本身，代码如下：

```php
function register_new_finder_category( $finder_categories_manager ) {

	$finder_categories_manager->register( new New_Finder_Category() );

};
add_action( 'elementor/finder/register', 'register_new_finder_category' );
```
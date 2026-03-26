---
title: "注册查找器类别"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Managers
    - Src
    - Repos
---

# 注册查找器类别

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

当你创建新的[查找器类别](src/finder)时，必须注册它们。这需要通过挂载到查找器管理器中的注册钩子，并传递一个新的查找器类别实例来完成。

## 注册新的查找器类别

开发者应使用以下代码来注册新的查找器类别：

```php
/**
 * 注册新的 Elementor 查找器类别。
 *
 * @param \Elementor\Core\Common\Modules\Finder\Categories_Manager $finder_categories_manager Elementor 查找器类别管理器。
 * @return void
 */
function register_new_finder_categories( $finder_categories_manager ) {

	require_once( __DIR__ . '/finder/finder-1.php' );
	require_once( __DIR__ . '/finder/finder-2.php' );

	$finder_categories_manager->register( new \Elementor_Finder_Category_1() );
	$finder_categories_manager->register( new \Elementor_Finder_Category_2() );

}
add_action( 'elementor/finder/register', 'register_new_finder_categories' );
```

这段代码挂载到 `elementor/finder/register` 动作钩子，该钩子持有查找器类别管理器。然后管理器通过传递查找器类别实例来注册新的查找器类别。
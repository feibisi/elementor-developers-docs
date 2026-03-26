---
title: "移除查找器分类"
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

# 移除查找器分类

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

开发者可以使用 `elementor/finder/categories` 过滤器钩子来移除整个查找器分类及其所有项目。

## 移除分类

在下面的示例中，我们将移除 "`edit`" 分类：

```php
function remove_elementor_finder_category( array $categories ) {

	unset( $categories['edit'] );
	return $categories;

}
add_filter( 'elementor/finder/categories', 'remove_elementor_finder_category' );
```

该过滤器钩子接受 `$categories` 参数，它本质上是一个查找器分类数组。我们可以从这个数组中筛选分类，并返回更新后的数组。
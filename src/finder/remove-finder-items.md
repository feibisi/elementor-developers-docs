---
title: "移除查找器项目"
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

# 移除查找器项目

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

开发者可以通过使用 `elementor/finder/categories` 过滤器钩子，从查找器类别中移除特定项目。

## 移除项目

在下面的示例中，我们将从 "`create`" 类别中移除 "`post`" 项目：

```php
function remove_elementor_finder_item( array $categories ) {

	unset( $categories['create']['items']['post'] );
	return $categories;

}
add_filter( 'elementor/finder/categories', 'remove_elementor_finder_item' );
```

`$categories` 参数包含所有类别及其项目。我们可以移除特定项目并返回更新后的数组。
---
title: "自定义查询过滤器"
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

# 自定义查询过滤器

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

**文章小工具**和**作品集小工具**都配备了强大的查询控件，可让您选择要在小工具中显示的特定文章。但有时，您需要对查询进行更多控制。针对这些情况，自定义查询过滤器应运而生，它公开了 [WP_Query](https://developer.wordpress.org/reference/classes/wp_query/) 对象，允许您以任意方式自定义查询。

## 钩子详情

* **钩子类型:** 动作钩子
* **钩子名称:** `elementor/query/{$query_id}`
* **影响范围:** 查询

## 钩子参数

| 参数 | 类型                       | 描述                   |
|------|----------------------------|-----------------------|
| `query`  | _`\WP_Query`_              | WordPress 查询实例。 |
| `widget` | _`\Elementor\Widget_Base`_ | 小部件实例。          |

## 设置自定义筛选器

<img :src="$withBase('/assets/img/elementor-posts-query-id.png')" alt="Elementor Posts Query ID" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

在文章或作品集小工具中，为您的查询设置一个ID，确保其唯一性，除非您希望筛选器在多个文章或作品集小工具上运行。

在以下示例中，查询ID设置为 `my_custom_filter`，因此当Elementor渲染小工具时，将基于该查询ID创建一个自定义筛选器：`elementor/query/my_custom_filter`。

## Using the Custom Filter

After you have set up the custom query filter, you can use it to modify the query in the same way that the WordPress native [pre_get_posts](https://developer.wordpress.org/reference/hooks/pre_get_posts/) hook lets you modify a query. Using the custom query filter is just like any other WordPress native action hook:

```php
/**
 * Update the posts widget or portfolio widget query.
 *
 * @since 1.0.0
 * @param \WP_Query $query The WordPress query instance.
 */
function custom_query_callback( $query ) {
	// Modify the posts query here
}
add_action( 'elementor/query/{$query_id}', 'custom_query_callback' );
```

## 示例

### 在文章小工具中显示多种文章类型

使用以下代码片段在文章小工具中显示多种文章类型：

```php
/**
 * 更新查询以使用特定的文章类型。
 *
 * @since 1.0.0
 * @param \WP_Query $query WordPress 查询实例。
 */
function my_query_by_post_types( $query ) {
	$query->set( 'post_type', [ 'custom-post-type1', 'custom-post-type2' ] );
}
add_action( 'elementor/query/{$query_id}', 'my_query_by_post_types' );
```

### Filter Posts by the Posts' Metadata in a Portfolio Widget

Use the code below to show posts with a metadata key filter in a portfolio widget:

```php
/**
 * Update the query by specific post meta.
 *
 * @since 1.0.0
 * @param \WP_Query $query The WordPress query instance.
 */
function my_query_by_post_meta( $query ) {

	// Get current meta Query
	$meta_query = $query->get( 'meta_query' );

	// If there is no meta query when this filter runs, it should be initialized as an empty array.
	if ( ! $meta_query ) {
		$meta_query = [];
	}

	// Append our meta query
	$meta_query[] = [
		'key' => 'project_type',
		'value' => [ 'design', 'development' ],
		'compare' => 'in',
	];

	$query->set( 'meta_query', $meta_query );

}
add_action( 'elementor/query/{$query_id}', 'my_query_by_post_meta' );
```

### 按评论数排序的帖子小工具中最受欢迎的文章

使用以下代码在帖子小工具中按评论数排序显示文章：

```php
/**
 * 按评论数对查询中的文章进行排序。
 *
 * @since 1.0.0
 * @param \WP_Query $query WordPress 查询实例。
 */
function my_query_by_different_order( $query ) {
	$query->set( 'orderby', 'comment_count' );
}
add_action( 'elementor/query/{$query_id}', 'my_query_by_different_order' );
```

### 在文章小部件中显示多种状态的文章

使用以下代码显示特定文章状态的文章：

注意：使用此代码片段可能导致显示私有数据，请谨慎使用。

```php
/**
 * 更新查询以使用特定的文章状态。
 *
 * @since 1.0.0
 * @param \WP_Query $query WordPress 查询实例。
 */
function my_query_by_post_status( $query ) {
	$query->set( 'post_status', [ 'future', 'draft'] );
}
add_action( 'elementor/query/{$query_id}', 'my_query_by_post_status' );
```

### 增加文章小工具中的文章数量

使用以下代码来更改文章小工具中显示的文章数量：

```php
/**
 * 更新查询以设置要显示的文章数量。
 *
 * @since 1.0.0
 * @param \WP_Query $query WordPress 查询实例。
 */
function my_query_posts_per_page( $query ) {
	$query->set( 'posts_per_page', 20 );
}
add_action( 'elementor/query/{$query_id}', 'my_query_posts_per_page' );
```

## 注意事项

您可能需要刷新[编辑器](src/editor)才能看到滤镜效果。
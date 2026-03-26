---
title: "占位图"
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

# 占位图

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/elementor-placeholder-image.png')" alt="Elementor Placeholder Image" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

Elementor 图片小部件和基于媒体的控件会显示占位图，除非用户从媒体库中选择特定图片。

默认情况下，Elementor 使用位于 Elementor 插件资源文件夹中的默认图片。但是，您可以用自定义图片替换此默认图片。

## 钩子详情

* **钩子类型：** 过滤器钩子
* **钩子名称：** `elementor/utils/get_placeholder_image_src`
* **影响范围：** 编辑器

## 占位图过滤器钩子

通过 `elementor/utils/get_placeholder_image_src` 过滤器钩子，开发者可以更改默认占位图的来源。

您可以从外部 URL 设置占位图：

```php
/**
 * 更改默认的 Elementor 占位图。
 *
 * 使用位于外部 URL 的图片。
 *
 * @since 1.0.0
 */
function custom_elementor_placeholder_image() {
	return 'https://developers.elementor.com/path/to/placeholder.png';
}
add_filter( 'elementor/utils/get_placeholder_image_src', 'custom_elementor_placeholder_image' );
```

或者设置位于您插件文件夹中的占位图：

```php
/**
 * 更改默认的 Elementor 占位图。
 *
 * 使用位于插件资源文件中的图片。
 *
 * @since 1.0.0
 */
function custom_elementor_placeholder_image() {
	return plugins_url( 'assets/images/placeholder.png', __FILE__ );
}
add_filter( 'elementor/utils/get_placeholder_image_src', 'custom_elementor_placeholder_image' );
```

**注意：** Elementor 使用的默认占位图位于："`plugins/elementor/assets/images/placeholder.png`"。
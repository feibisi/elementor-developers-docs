---
title: "Description Meta Tag"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Hello Elementor Theme
    - Src
    - Repos
---

# Description Meta Tag

<Badge type="tip" vertical="top" text="Hello Elementor Theme" /> <Badge type="warning" vertical="top" text="Basic" />

为了在不使用外部插件的情况下改善 SEO，主题会添加一个包含页面/文章摘要的 [meta 标签](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)。开发者可以通过一个简单的钩子来移除这个 meta 标签。

## 钩子详情

* **钩子类型:** 动作钩子
* **钩子名称:** `hello_elementor_add_description_meta_tag`

该钩子会在具有摘要的单篇文章页面中，向 `<head>` 添加 HTML `<meta>` 标签：

```html
<meta name="description" content="..." />
```

搜索引擎、社交媒体和其他外部网站会使用 `<title>` 和描述 `<meta>` 标签中的数据。

然而，如果网站选择使用外部 SEO 插件，页面可能会出现重复的描述 meta 标签。为了避免这种情况，SEO 插件可以移除由主题添加的描述 meta 标签。

## 使用方法

要阻止主题显示带有页面描述的 `<meta>` 标签，请使用以下代码：

```php
function remove_hello_elementor_description_meta_tag() {
	remove_action( 'wp_head', 'hello_elementor_add_description_meta_tag' );
}
add_action( 'after_setup_theme', 'remove_hello_elementor_description_meta_tag' );
```
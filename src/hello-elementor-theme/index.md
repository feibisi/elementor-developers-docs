---
title: "Hello Elementor 主题"
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

# Hello Elementor 主题

<Badge type="tip" vertical="top" text="Hello Elementor Theme" /> <Badge type="warning" vertical="top" text="Basic" />

Hello Elementor Theme 是一款轻量级、极简风格的 WordPress 主题，专为配合 Elementor 页面构建器插件而设计。该主题提供了多个功能，开发者可以通过 WordPress 钩子进行控制。

## 可用的过滤器钩子

该主题提供了多个过滤器钩子，可用于子主题的 `functions.php` 文件中，以修改默认设置。

### 功能钩子

* [注册文章类型功能](src/hello-elementor-theme/hello_elementor_post_type_support)
* [注册主题功能](src/hello-elementor-theme/hello_elementor_add_theme_support)
* [注册导航菜单](src/hello-elementor-theme/hello_elementor_register_menus)
* [注册 WooCommerce 功能](src/hello-elementor-theme/hello_elementor_add_woocommerce_support)
* [注册 Elementor 主题位置](src/hello-elementor-theme/hello_elementor_register_elementor_locations)

### 样式钩子

* [加载样式](src/hello-elementor-theme/hello_elementor_enqueue_style)
* [加载主题样式](src/hello-elementor-theme/hello_elementor_enqueue_theme_style)

### 内容钩子

* [内容宽度](src/hello-elementor-theme/hello_elementor_content_width)
* [页面标题](src/hello-elementor-theme/hello_elementor_page_title)
* [视口内容](src/hello-elementor-theme/hello_elementor_viewport_content)
* [描述元标签](src/hello-elementor-theme/hello_elementor_add_description_meta_tag)
* [启用跳过链接](src/hello-elementor-theme/hello_elementor_enable_skip_link)
* [跳过链接 URL](src/hello-elementor-theme/hello_elementor_skip_link_url)
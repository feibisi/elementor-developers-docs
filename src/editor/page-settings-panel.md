---
title: "页面设置面板"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor
    - Src
    - Repos
---

# 页面设置面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/page-settings-panel.png')" alt="Elementor Page Settings Panel" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

**页面设置**是[编辑器](src/editor)中的一个面板，用户可以在其中更改文章/页面的字段，例如标题、摘要（如果文章类型支持摘要）、特色图像、文章状态等。

页面设置基于文章/页面，这意味着网站上的每个文章/页面都有其独特的设置，这些设置保存在数据库的 `wp_posts` 表中。

## 结构与功能

该面板包含三个标签页：

* **设置** - 管理常规页面设置。
* **样式** - 管理页面样式。
* **高级** - 管理其他页面设置。

设置面板相当于 Elementor 中的 WordPress 文章/页面编辑界面。您可以在此设置页面标题、摘要、特色图像等。

样式设置用于在页面级别添加新样式，这与控制全站样式的站点设置不同。例如，用户可以更改页面背景颜色/图像，覆盖站点背景样式。

在高级标签页中，用户可以添加仅在此页面加载的自定义 CSS。

## 检索已保存的数据

设置选项卡中的数据是常规的 WordPress 页面/文章数据，可以使用常规的主题函数进行检索。

```php
// 检索页面数据
$page_id        = get_the_ID();
$page_title     = get_the_title();
$page_excerpt   = get_the_excerpt();
$page_author    = get_the_author();
$page_permalink = get_permalink();
$page_thumbnail = get_the_post_thumbnail();
```

样式选项卡中的数据保存在页面的 `post meta` 中。这个 `post meta` 包含了与文档设置相关的大部分设置（不包括一些需要特殊处理的设置）。

```php
// 检索页面设置管理器
$page_settings_manager = \Elementor\Core\Settings\Manager::get_settings_managers( 'page' );

// 检索当前页面的设置模型
$page_settings_model = $page_settings_manager->get_model( $page_id );

// 从自定义控件检索数据
$test_color = $page_settings_model->get_settings( 'test_color' );

echo $test_color; // 可能的输出: '#9b0a46'
```

## Adding New Settings

Developers can add new controls to this panel. This is done by [injecting controls](src/hooks/injecting-controls) into page settings.

Below is an example how we can add color control to the style tab:

```php
/**
 * Register additional document controls.
 *
 * @param \Elementor\Core\DocumentTypes\PageBase $document The PageBase document instance.
 */
function register_document_controls( $document ) {

    if ( ! $document instanceof \Elementor\Core\DocumentTypes\PageBase || ! $document::get_property( 'has_elements' ) ) {
        return;
    }

    $document->start_controls_section(
        'test_section',
        [
            'label' => esc_html__( 'Test Section', 'textdomain' ),
            'tab' => \Elementor\Controls_Manager::TAB_STYLE,
        ]
    );

	$document->add_control(
		'test_color',
		[
			'label' => esc_html__( 'Test Color', 'textdomain' ),
			'type' => \Elementor\Controls_Manager::COLOR,
			'selectors' => [
				'{{WRAPPER}}' => 'background-color: {{VALUE}}',
			],
		]
	);

    $document->end_controls_section();
}
add_action( 'elementor/documents/register_controls', 'register_document_controls' );
```

In the page settings scope, the `{ { WRAPPER } }` placeholder represents a unique class of the `<body>` element.
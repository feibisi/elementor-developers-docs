---
title: "Elementor 选项卡"
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

# Elementor 选项卡

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/elementor-tabs.png')" alt="Elementor Tabs" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

在某些面板中，Elementor 使用选项卡导航来显示控件。扩展 Elementor 时，您可以使用任何所需的选项卡，或创建新的选项卡。

## Built-in Tabs

Elementor has 6 pre-defined tabs used in different panels:

| Name/ID      | Label      | Constant                                      |
|--------------|------------|-----------------------------------------------|
| `content`    | Content    | `\Elementor\Controls_Manager::TAB_CONTENT`    |
| `style`      | Style      | `\Elementor\Controls_Manager::TAB_STYLE`      |
| `advanced`   | Advanced   | `\Elementor\Controls_Manager::TAB_ADVANCED`   |
| `responsive` | Responsive | `\Elementor\Controls_Manager::TAB_RESPONSIVE` |
| `layout`     | Layout     | `\Elementor\Controls_Manager::TAB_LAYOUT`     |
| `settings`   | Settings   | `\Elementor\Controls_Manager::TAB_SETTINGS`   |

The tabs are set in the `\Elementor\Controls_Manager` class. They are defined as constants and registered using the `init_tabs()` method; each constant contains the tab name and label.

## 使用示例

例如，[小部件面板](src/editor/widgets-panel)在**内容选项卡**中显示控件，允许用户设置小部件内容，并在**样式选项卡**中设计内容。此外，Elementor 为所有小部件添加了一个**高级选项卡**。

另一方面，[页面设置面板](src/editor/page-settings-panel)根据具体设置，在**设置选项卡**、**样式选项卡**、**布局选项卡**等中显示控件。

## 使用选项卡

当我们在元素面板中添加新控件时，会使用继承的 `add_control()` 方法。在添加新控件之前，我们需要使用 `start_controls_section()` 方法创建一个新部分。我们使用此方法来定义选项卡：

```php {5}
$this->start_controls_section(
	'style_section',
	[
		'label' => esc_html__( '样式部分', 'textdomain' ),
		'tab' => \Elementor\Controls_Manager::TAB_STYLE,
	]
);
```

## 添加新标签页

要创建自定义标签页，请使用 `add_tab()` 方法：

```php
function add_panel_tab() {
	\Elementor\Controls_Manager::add_tab(
		'new-tab',
		esc_html__( 'New Tab', 'textdomain' )
	);
}
add_action( 'elementor/init', 'add_panel_tab' );
```

若要在标签页标签上方添加自定义图标，您需要添加自定义 CSS：

```css
.elementor-panel .elementor-tab-control-new-tab a:before,
.elementor-panel .elementor-tab-control-new-tab span:before {
	font-family: eicons;
	content: '\e942';
}
```

## 最佳实践

::: warning 官方指南
Elementor 官方指南强烈建议使用默认标签页之一。
:::

尽管如此，此功能仍被记录在案，因为部分插件作者会使用代码变通方案，这些方案会降低编辑器速度，并在某些极端情况下导致其崩溃。
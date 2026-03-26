---
title: "默认面板"
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

# 默认面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

默认情况下，当编辑器首次加载时，Elementor 会显示[小部件面板](src/editor/widgets-panel)。您可以更改此设置。

## 更改默认面板

使用以下代码将[页面设置面板](src/editor/page-settings-panel)设为默认面板：

```php
function change_default_elementor_panel( $config ) {

	$config = array_replace_recursive(
		$config,
		[
			'panel' => [
				'default_route' => 'panel/page-settings/settings'
			]
		]
	);

	return $config;

}
add_filter( 'elementor/document/config', 'change_default_elementor_panel' );
```

## 可用面板

以下是您可以用作默认面板的内置面板的部分列表：

* [菜单面板](src/editor/menu-panel)
  * `panel/menu`
* [用户偏好设置](src/editor/user-preferences-panel)
  * `panel/editor-preferences`
* [页面设置](src/editor/page-settings-panel)
  * `panel/page-settings/settings`
  * `panel/page-settings/style`
  * `panel/page-settings/advanced`
* [历史面板](src/editor/history-panel)
  * `panel/history/actions`
  * `panel/history/revisions`
* [小部件面板](src/editor/widgets-panel)
  * `panel/elements/categories`
  * `panel/elements/global`
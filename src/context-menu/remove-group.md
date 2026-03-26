---
title: "移除群组"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Context Menu
    - Src
    - Repos
---

# 移除群组

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

要从上下文菜单中移除群组，我们需要检查该群组是否存在于相关的菜单类型中，并从上下文菜单中删除该群组。这将删除整个群组以及分配给该群组的所有操作。

## 移除小部件群组

在下面的示例中，我们将从 `widgets` 上下文菜单中移除 `custom-widget-actions` 群组：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'widget' === elementType ) {
		const groupIndex = customGroups.findIndex( ( group ) => 'custom-widget-actions' === group.name );
		if ( groupIndex > -1 ) {
			customGroups.splice( groupIndex, 1 );
		}
	}

	return customGroups;

} );
```

## 移除列群组

现在我们将从 `columns` 上下文菜单中移除 `custom-column-actions` 群组：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'column' === elementType ) {
		const groupIndex = customGroups.findIndex( ( group ) => 'custom-column-actions' === group.name );
		if ( groupIndex > -1 ) {
			customGroups.splice( groupIndex, 1 );
		}
	}

	return customGroups;

} );
```

## 移除区块群组

接下来我们将从 `section` 上下文菜单中移除 `custom-section-actions` 群组：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'section' === elementType ) {
		const groupIndex = customGroups.findIndex( ( group ) => 'custom-section-actions' === group.name );
		if ( groupIndex > -1 ) {
			customGroups.splice( groupIndex, 1 );
		}
	}

	return customGroups;

} );
```
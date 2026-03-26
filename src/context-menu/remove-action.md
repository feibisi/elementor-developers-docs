---
title: "移除操作"
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

# 移除操作

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

要从上下文菜单中移除一个现有的操作，我们需要从某个组中删除该操作。

## 移除小部件操作

在下面的示例中，我们将从位于 `widget` 上下文菜单中的 `custom-widget-actions` 组中移除 `widget-action` 操作：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'widget' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-widget-actions' === group.name ) {
				const actionIndex = group.actions.findIndex( ( action ) => 'widget-action' === action.name );
				if ( actionIndex > -1 ) {
					group.actions.splice( actionIndex, 1 );
				}
			}
		} );
	}

	return customGroups;

} );
```

## 移除列操作

现在我们将从位于 `column` 上下文菜单中的 `custom-column-actions` 组中移除 `column-action` 操作：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'column' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-column-actions' === group.name ) {
				const actionIndex = group.actions.findIndex( ( action ) => 'column-action' === action.name );
				if ( actionIndex > -1 ) {
					group.actions.splice( actionIndex, 1 );
				}
			}
		} );
	}

	return customGroups;

} );
```

## 移除区块操作

接下来我们将从位于 `section` 上下文菜单中的 `custom-section-actions` 组中移除 `section-action` 操作：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'section' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-section-actions' === group.name ) {
				const actionIndex = group.actions.findIndex( ( action ) => 'section-action' === action.name );
				if ( actionIndex > -1 ) {
					group.actions.splice( actionIndex, 1 );
				}
			}
		} );
	}

	return customGroups;

} );
```
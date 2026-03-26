---
title: "更新群组"
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

# 更新群组

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

要修改一个已存在的群组，我们需要更改群组对象。

## 更新小部件群组

在下面的示例中，我们将简单地将 `widget` 上下文菜单中的群组名称从 `custom-widget-actions` 重命名为 `new-name`：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'widget' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-widget-actions' === group.name ) {
				group.name = 'new-name';
			}
		} );
	}

	return customGroups;

} );
```

## 更新列群组

接下来，我们将移除 `column` 上下文菜单中 `custom-column-actions` 群组内的所有操作：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'column' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-column-actions' === group.name ) {
				group.actions = {};
			}
		} );
	}

	return customGroups;

} );
```

## 更新区块群组

现在我们将更新 `section` 上下文菜单。在 `custom-section-actions` 群组内，我们将更改 `section-action-1` 操作的图标：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'section' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-section-actions' === group.name ) {
				group.actions.forEach( ( action ) => {
					if ( 'section-action-1' === action.name ) {
						action.icon = 'eicon-code';
					}
				} );
			}
		} );
	}

	return customGroups;

} );
```
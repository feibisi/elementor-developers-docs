---
title: "更新操作"
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

# 更新操作

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

要修改一个现有的操作，我们需要更改特定条目中的操作对象值。

## 更新小部件操作

在下面的示例中，我们将更新 `widget-action` 操作的图标：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'widget' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-widget-actions' === group.name ) {
				group.actions.forEach( ( action ) => {
					if ( 'widget-action' === action.name ) {
						action.icon = 'eicon-code';
					}
				} );
			}
		} );
	}

	return customGroups;

} );
```

## 更新列操作

现在我们将更新 `column-action` 操作的标题标签：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'column' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-column-actions' === group.name ) {
				group.actions.forEach( ( action ) => {
					if ( 'column-action' === action.name ) {
						action.title = 'New Label';
					}
				} );
			}
		} );
	}

	return customGroups;

} );
```

## 更新区块操作

接下来我们将更新整个 `section-action` 操作：

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	if ( 'column' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-column-actions' === group.name ) {
				group.actions.forEach( ( action ) => {
					if ( 'column-action' === action.name ) {
						action.icon = 'eicon-alert';
						action.title = 'Hellooo';
						action.callback = () => alert( 'bla bla' );
					}
				} );
			}
		} );
	}

	return customGroups;

} );
```
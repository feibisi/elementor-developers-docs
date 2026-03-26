---
title: "添加新操作"
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

# 添加新操作

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

要向上下文菜单添加新操作，我们需要定义一个新的操作对象，并将该对象插入到相关的上下文菜单组中。

## 添加新小部件操作

在下面的示例中，我们将向现有的 `custom-widget-actions` 组添加一个新操作。此操作将添加一个指向 Elementor 网站的外部链接。

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	const newAction = {
		name: 'elementor-link',
		icon: 'eicon-alert',
		title: 'Elementor Link',
		isEnabled: () => true,
		callback: () => window.open( 'https://elementor.com/', '_blank' ).focus(),
	};

	if ( 'widget' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-widget-actions' === group.name ) {
				group.actions.push( newAction );
			}
		} );
	}

	return customGroups;

} );
```

## 添加新列操作

现在我们将向现有的 `custom-column-actions` 组添加一个新操作。此操作将在浏览器控制台中记录一些文本。

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	const newAction = {
		name: 'log',
		icon: 'eicon-code',
		title: 'Some Console Log',
		isEnabled: () => true,
		callback: () => console.log( 'some text...' ),
	};

	if ( 'column' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-column-actions' === group.name ) {
				group.actions.push( newAction );
			}
		} );
	}

	return customGroups;

} );
```

## 添加新区块操作

接下来，我们将向现有的 `custom-section-actions` 组添加一个新操作。此操作将打开页面设置面板。

```js
elementor.hooks.addFilter( 'elements/context-menu/groups', ( customGroups, elementType ) => {

	const newAction = {
		name: 'page-settings',
		icon: 'eicon-cog',
		title: 'Page Settings',
		isEnabled: () => true,
		callback: () => $e.run( 'panel/page-settings/settings' ),
	};

	if ( 'section' === elementType ) {
		customGroups.forEach( ( group ) => {
			if ( 'custom-section-actions' === group.name ) {
				group.actions.push( newAction );
			}
		} );
	}

	return customGroups;

} );
```
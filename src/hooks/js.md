---
title: "JS Hooks"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Hooks
    - Src
    - Repos
---

# JS Hooks

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor has a number of JS hooks that allow developers to change default behavior and even add new functionality.

## 前端过滤器

### `frontend/handlers/menu_anchor/scroll_top_distance`

应用于菜单锚点小部件，设置自定义顶部距离

#### Arguments

| Argument    | Type            | Description                                                              |
|-------------|-----------------|--------------------------------------------------------------------------|
| `scrollTop` | _`integer`_     | The default scrollTop. It only takes the WordPress admin bar into account|

#### Example

```js
jQuery( function( $ ) {
	// Add space for Elementor Menu Anchor link
	if ( window.elementorFrontend ) {
		elementorFrontend.hooks.addFilter( 'frontend/handlers/menu_anchor/scroll_top_distance', function( scrollTop ) {
			return scrollTop - 30;
		} );
	}
} );

add_action( 'wp_footer', function() {
 if ( ! defined( 'ELEMENTOR_VERSION' ) ) {
 return;
 }
	?>
	<script>
 jQuery( function( $ ) {
 // Add space for Elementor Menu Anchor link
 if ( window.elementorFrontend ) {
 elementorFrontend.hooks.addFilter( 'frontend/handlers/menu_anchor/scroll_top_distance', function( scrollTop ) {
 return scrollTop - 30;
 } );
 }
 } );
	</script>
	<?php
} );
```

## 前端操作

### `elementor/frontend/init`

加载 Elementor 前端。

#### Arguments

None

#### Example

```js
elementorFrontend.hooks.addAction( 'elementor/frontend/init', function() {
 // Do something that is based on the elementorFrontend object.
} );
```

### `frontend/element_ready/global`

当每个元素（包括节和列）准备就绪时运行。

#### 参数

| 参数       | 类型                                        | 描述 |
|------------|---------------------------------------------|------|
| `$scope`   | _`当前元素，已用 jQuery 包装`_              |      |
| `$`        | _`jQuery 实例`_                             |      |

#### 示例

```js
elementorFrontend.hooks.addAction( 'frontend/element_ready/global', function( $scope ) {
	if ( $scope.data( 'shake' ) ){
		$scope.shake();
	}
} );
```

### `frontend/element_ready/widget`

在每个部件准备就绪时运行。

#### Arguments

| Argument   | Type                                        | Description |
|------------|---------------------------------------------|-------------|
| `$scope`   | _`The current element wrapped with jQuery`_ |             |
| `$`        | _`The jQuery instance`_                     |             |

#### 示例

```js
elementorFrontend.hooks.addAction( 'frontend/element_ready/widget', function( $scope ) {
	if ( $scope.data( 'shake' ) ){
		$scope.shake();
	}
} );
```

### `frontend/element_ready/{elementType.skinName}`

当特定元素类型及其皮肤准备就绪时运行。

#### Arguments

| Argument   | Type                                        | Description |
|------------|---------------------------------------------|-------------|
| `$scope`   | _`The current element wrapped with jQuery`_ |             |
| `$`        | _`The jQuery instance`_                     |             |

#### Example

```js
// For a widget without a skin (skin = default)
elementorFrontend.hooks.addAction( 'frontend/element_ready/image.default', function( $scope ) {
	if ( $scope.find( 'a' ) ){
		$scope.find( 'a' ).lightbox();
	}
} );

// For a widget with a skin named `satellite`
elementorFrontend.hooks.addAction( 'frontend/element_ready/google-maps.satellite', function( $scope ) {
	var $iframe = $scope.find( 'iframe' );
	var $iframeUrl = $iframe.attr( 'src' );
	$iframe.attr( 'src', $iframeUrl + '&maptype=satellite' );
} );
```

## 编辑器钩子

### `panel/open_editor/{elementType}`

当打开设置面板以编辑元素时应用。

#### Arguments

| Argument | Type       | Description                  |
|----------|------------|------------------------------|
| `panel`  | _`object`_ | The panel object             |
| `model`  | _`object`_ | The backbone model instance  |
| `view`   | _`object`_ | The backbone view instance   |

#### Example

```js
elementor.hooks.addAction( 'panel/open_editor/widget', function( panel, model, view ) {
	if ( 'section' !== model.elType && 'column' !== model.elType ) {
		return;
	}
   var $element = view.$el.find( '.elementor-selector' );

   if ( $element.length ) {
   	$element.click( function() {
   	  alert( 'Some Message' );
   	} );
   }
} );
```

### `panel/open_editor/{elementType}/{elementName}`

当打开设置面板以编辑特定元素名称时应用。

#### 参数

| 参数     | 类型         | 描述                     |
|----------|--------------|--------------------------|
| `panel`  | _`object`_   | 面板对象                 |
| `model`  | _`object`_   | Backbone 模型实例        |
| `view`   | _`object`_   | Backbone 视图实例        |

#### Example

```js
elementor.hooks.addAction( 'panel/open_editor/widget/slider', function( panel, model, view ) {
   var $element = view.$el.find( '.elementor-selector' );

   if ( $element.length ) {
   	$element.click( function() {
   	  alert( 'Some Message' );
   	} );
   }
} );
```
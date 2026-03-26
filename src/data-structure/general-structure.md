---
title: "通用结构"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Data Structure
    - Src
    - Repos
---

# 通用结构

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

JSON 结构包含一个对象，其中存储了页面相关信息。这些信息包括文档类型、标题和版本。此外，它还包含实际数据，例如文档设置和文档内容。

## JSON Structure

Basic structure:

```json
{
	"title": "Template Title",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": []
}
```

## JSON Values

| Argument        | Type                 | Description |
|-----------------|----------------------|-------------|
| `title`         | _`string`_           | The title displayed to the user in the WordPress dashboard and the Elementor Editor. |
| `type`          | _`string`_           | The document type. Available values are: `header`, `footer`, `error-404`, `popup`, `page`, `post`, etc. |
| `version`       | _`string`_           | The data structure version. The latest version is `0.4`. |
| `page_settings` | _`array`_/_`object`_ | Data from the "Page Setting" panel. An empty `array` if settings are not defined, an `object` if the page has settings. |
| `content`       | _`array`_            | An array of objects that holds all the page elements. |

## Examples

### Header JSON Example

A "header" template with custom page settings and a single element.

```json
{
	"title": "Site Header",
	"type": "header",
	"version": "0.4",
	"page_settings": {
		"content_wrapper_html_tag": "header",
		"background_background": "classic",
		"background_color": "#000000"
	},
	"content": [
		{
			"id": "3130e2cf",
			"elType": "container",
			"isInner": false,
			"settings": [],
			"elements": []
		}
	]
}
```

### Footer JSON Example

A "footer" template with a single container element.

```json
{
	"title": "Site Footer",
	"type": "footer",
	"version": "0.4",
	"page_settings": {
		"content_wrapper_html_tag": "footer"
	},
	"content": [
		{
			"id": "1aebaeaa",
			"elType": "container",
			"isInner": false,
			"settings": [],
			"elements": []
		}
	]
}
```

### 404 页面 JSON 示例

一个带有自定义背景色的 "404 页面"：

```json
{
	"title": "404 Page",
	"type": "error-404",
	"version": "0.4",
	"page_settings": {
		"content_wrapper_html_tag": "main",
		"background_background": "classic",
		"background_color": "#333333"
	},
	"content": []
}
```

### 弹窗 JSON 示例

一个用于移动导航的弹窗，包含一些与弹窗相关的设置：

```json
{
	"title": "Mobile Navigation Popup",
	"type": "popup",
	"version": "0.4",
	"page_settings": {
		"width": {
			"unit": "px",
			"size": 600,
			"sizes": []
		},
		"entrance_animation": "fadeIn",
		"exit_animation": "fadeIn",
		"overlay_background_color": "#000000AA",
		"prevent_scroll": "yes"
	},
	"content": [
		{
			"id": "c647ac2",
			"elType": "container",
			"isInner": false,
			"settings": {
				"padding": {
					"unit": "px",
					"top": "20",
					"right": "20",
					"bottom": "20",
					"left": "20",
					"isLinked": true
				}
			},
			"elements": []
		}
	]
}
```
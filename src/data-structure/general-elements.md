---
title: "通用元素"
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

# 通用元素

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

每个 Elementor 元素，无论是布局元素（区块、列、容器）还是小部件元素，都拥有一组基本信息。这些数据在创建页面时用于解析元素。

## JSON 结构

基本元素结构：

```json
{
	"id": "12345678",
	"elType": "element",
	"isInner": false,
	"settings": [],
	"elements": []
}
```

## JSON 值

| 参数       | 类型                 | 描述 |
|------------|----------------------|-------------|
| `id`       | _`string`_           | 代表该元素的唯一标识键。 |
| `elType`   | _`string`_           | 元素类型。 |
| `isInner`  | _`boolean`_          | 该元素是否为内部元素。 |
| `settings` | _`array`_/_`object`_ | 来自面板的元素数据，保存着编辑器控件的值。如果未定义设置，则为空 `array`；如果元素有设置，则为 `object`。 |
| `elements` | _`array`_            | 一个包含所有嵌套元素的对象数组。 |

根据元素类型，可以引入额外的值。例如，当 `elType` 为 `widget` 时，会添加一个额外的 `widgetType` 值来指示[部件名称](src/widgets/widget-data)（例如 `heading`、`image`、`button`、`social-icons` 等）。

## 布局元素与部件元素

Elementor 支持的两大主要元素类型是布局元素和部件元素。布局元素（区块、列、容器）可能存储关于嵌套 `elements` 的数据，而部件元素主要存储关于部件 `settings` 的数据。

## Examples

### A Page with Containers

An example of a page that has two empty containers:

```json
{
	"title": "Sample Page",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "6af611eb",
			"elType": "container",
			"isInner": false,
			"settings": [],
			"elements": []
		},
		{
			"id": "7fb170b9",
			"elType": "container",
			"isInner": false,
			"settings": [],
			"elements": []
		}
	]
}
```

### A Page with Nested Container

An example of a page that has a container element with nested containers:

```json
{
	"title": "Test Page",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "458aabdc",
			"elType": "container",
			"isInner": false,
			"settings": [],
			"elements": [
				{
					"id": "46ef0576",
					"elType": "container",
					"isInner": false,
					"settings": [],
					"elements": [
						{
							"id": "4a59f2e3",
							"elType": "container",
							"isInner": false,
							"settings": [],
							"elements": []
						}
					]
				}
			]
		}
	]
}
```

### A Page with Widgets

An example of a page that has a container element with three nested widgets:

```json
{
	"title": "About Page",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "6af611eb",
			"elType": "container",
			"isInner": false,
			"settings": [],
			"elements": [
				{
					"id": "6a637978",
					"elType": "widget",
					"widgetType": "heading",
					"isInner": false,
					"settings": {
						"title": "Add Your Heading Text Here",
						"align": "center"
					},
					"elements": []
				},
				{
					"id": "687dba89",
					"elType": "widget",
					"widgetType": "image",
					"isInner": false,
					"settings": {
						"_padding": {
							"unit": "px",
							"top": "100",
							"right": "0",
							"bottom": "100",
							"left": "0",
							"isLinked": false
						}
					},
					"elements": []
				},
				{
					"id": "6f58bb5",
					"elType": "widget",
					"widgetType": "button",
					"isInner": false,
					"settings": {
						"text": "Click Me",
						"button_text_color": "#000000",
						"background_color": "#E7DFF5"
					},
					"elements": []
				}
			]
		}
	]
}
```
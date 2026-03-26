---
title: "小部件元素"
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

# 小部件元素

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 小部件是一个拥有自定义属性的元素。小部件对象包含元素 ID、元素类型、小部件类型以及基于小部件控件的所有元素设置等信息。

## JSON 结构

Widget 元素结构：

```json
{
	"id": "12345678",
	"elType": "widget",
	"widgetType": "heading",
	"isInner": false,
	"settings": [],
	"elements": []
}
```

## JSON 值

| 参数         | 类型                 | 描述 |
|--------------|----------------------|-------------|
| `id`         | _`string`_           | 代表该元素的唯一标识键。 |
| `elType`     | _`string`_           | 元素类型。 |
| `widgetType` | _`string`_           | Widget 类型。 |
| `isInner`    | _`boolean`_          | 该元素是否为内部元素。 |
| `settings`   | _`array`_/_`object`_ | 来自面板的元素数据，保存了编辑器控件的值。如果未定义设置，则为空 `array`；如果元素有设置，则为 `object`。 |
| `elements`   | _`array`_            | 一个包含所有嵌套元素的对象数组。 |

## 嵌套元素

最初，Elementor 小部件不支持嵌套功能。最近，Elementor 开始探索允许嵌套功能的新方法。新的“菜单”小部件已支持嵌套功能，我们计划发布支持嵌套功能的“手风琴”、“选项卡”、“轮播”及其他小部件。

## 控件数据

每个控件都有一组自定义设置项。当用户将控件拖入页面并设置自定义值时，这些信息会以键值对形式保存在 `settings` 对象中。控件 ID 作为键名，数据作为键值。

## Examples

### A Page with Widgets

An example of a page that has a container element with three nested containers:

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
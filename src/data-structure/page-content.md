---
title: "页面内容"
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

# 页面内容

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

页面内容是一个 `array` 类型的对象数组，它保存了页面上的所有元素。此字段是递归的，意味着它可以包含嵌套元素，即元素内部可以包含其他元素。容器元素可以包含其他容器和小部件，而嵌套的小部件也可以包含其他小部件。

## JSON 结构

如果页面没有内容，`content` 是一个空 `array`：

```json
{
	"title": "Template Title",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": []
}
```

如果页面有内容，`content` 包含一个对象列表：

```json
{
	"title": "Template Title",
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
		}
	]
}
```

## Page Elements

Elements are simple objects containing element data. Some elements can have nested elements inside of them, others don't.

This is important as in the past Elementor had a strict data structure - the traditional structure. The page had "section" elements, sections had nested "column" elements, and the columns had "widget" elements.

With the introduction of containers, Elementor replaced the traditional data structure with a modern structure, allowing the user to nest multiple elements one inside the other.

Traditional structure:

<img :src="$withBase('/assets/img/data-structure-traditional.png')" alt="Traditional structure">

Modern structure:

<img :src="$withBase('/assets/img/data-structure-modern.png')" alt="Modern structure">

With the adoption of nested layout elements, Elementor introduced widgets with nested capabilities. Widgets like the nested "Tabs", nested "Accordion", nested "Carousel", and nested "Menu" (mega menu).

## Examples

### A Page with a Section and a Column

An example of a page that uses the traditional section-column-widget structure:

```json
{
	"title": "Sample Page",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "123ab956",
			"elType": "section",
			"isInner": false,
			"settings": [],
			"elements": [
				{
					"id": "1d4a679a",
					"elType": "column",
					"isInner": false,
					"settings": [],
					"elements": [
						{
							"id": "1d4a679a",
							"elType": "widget",
							"widgetType": "image",
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

### A Page with a Container

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

### A Page with Nested Containers

An example of a page that has a container element with several nested containers:

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

### A Page with a few Widgets

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
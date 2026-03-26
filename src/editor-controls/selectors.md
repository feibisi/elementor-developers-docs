---
title: "CSS 选择器"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor Controls
    - Src
    - Repos
---

# CSS 选择器

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

为了将控件值转换为 CSS 样式，Elementor 对分组控件使用 `selector` 参数，对其他控件使用 `selectors` 参数。这两个参数定义了使用哪些 CSS 选择器以及将值设置到哪些 CSS 属性上。让我们看看它是如何工作的。

## 自定义样式表

当创建 WordPress 文章/页面时，系统会为其分配一个唯一的 `id`。Elementor 编辑器利用此 `id`，根据每个控件的用户数据为该页面生成高度特定的样式表。随后，每次页面加载时，Elementor 都会加载属于该特定页面的样式表。

### 样式表路径

样式表保存在 `/elementor/css/` 文件夹中，该文件夹位于 WordPress 的 `/uploads/` 文件夹内。文件本身可通过其 `id` 来识别。

```
https://example.com/wp-content/uploads/elementor/css/post-{id}.css
```

当页面加载时，Elementor 会自动加载对应的样式表，其中包含从该页面小部件使用的控件中获取的样式选项。

### 自定义 CSS

编辑器控件允许用户输入内容或样式数据。要将控件值转换为 CSS 样式，控件需告知编辑器需要创建 CSS。这通过指定 CSS 选择器、属性和值的列表来实现。

```php
'selectors' => [
	'.css-selectors' => 'css-property: css-value;',
],
```

## Selector Arguments

Elementor has two selector arguments. The first is applied on group controls, the second on non-group controls. Both methods convert user data into a CSS style in a stylesheet.

### Group Controls

To convert group control data to a specific CSS selector:

```php{5,13}
$this->add_group_control(
	\Elementor\Group_Control_Background::get_type(),
	[
		'name' => 'background',
		'selector' => '{{WRAPPER}} .css-selector',
	]
);

$this->add_group_control(
	\Elementor\Group_Control_Background::get_type(),
	[
		'name' => 'background_hover',
		'selector' => '{{WRAPPER}}:hover .css-selector',
	]
);
```

The `selector` argument is a `string`. It is passed to all the inner controls in the group popup. When using group controls without specifying the `selector` argument, Elementor will use `{ { WRAPPER } }` as a fallback.

### 非分组控件

要将非分组控件数据转换为 CSS 选择器：

```php{6-8}
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .css-selector' => 'css-property: {{VALUE}};',
		],
	]
);
```

`selectors` 参数是一个 `array`。它可以接受单个或多个键值对。

## 选择器变体

在大多数情况下，单个选择器就足够了：

```php{6-8}
$this->add_control(
	'text-color',
	[
		'label' => esc_html__( 'Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .custom-container' => 'color: {{VALUE}};',
		],
	]
);
```

选择器也可以用于在单个选择器中指定多个 CSS 属性：

```php{6-8}
$this->add_control(
	'text-color',
	[
		'label' => esc_html__( 'Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .custom-container' => 'color: {{VALUE}}; border-color: {{VALUE}}; outline-color: {{VALUE}};',
		],
	]
);
```

或者在单个控件选择器中使用多个（逗号分隔的）CSS 选择器：

```php{6-8}
$this->add_control(
	'text-color',
	[
		'label' => esc_html__( 'Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .custom-container .heading, {{WRAPPER}} .custom-container .content' => 'color: {{VALUE}};',
		],
	]
);
```

上面的代码可以写成多个选择器：

```php{6-9}
$this->add_control(
	'text-color',
	[
		'label' => esc_html__( 'Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .custom-container .heading' => 'color: {{VALUE}};',
			'{{WRAPPER}} .custom-container .content' => 'color: {{VALUE}};',
		],
	]
);
```

为了同时支持 LTR 和 RTL 网站，您可以根据书写方向指定不同的选择器值：

```php{6-9}
$this->add_control(
	'gap-size',
	[
		'label' => esc_html__( 'Gap', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::NUMBER,
		'selectors' => [
			'body:not(.rtl) {{WRAPPER}} .custom-container' => 'padding-left: {{VALUE}}',
			'body.rtl {{WRAPPER}} .custom-container' => 'padding-right: {{VALUE}}',
		],
	]
);
```

## 作用域样式

Elementor 提供了两种在部件内部特定元素上应用自定义 CSS 的方法。它使用 `{ { WRAPPER } }` 或 `{ { ID } }` 关键字来实现作用域样式。这两个关键字都放置在键值对的左侧。

### 元素包装器

当选择器中使用元素包装器变量时：

```php
'selectors' => [
	'{{WRAPPER}} .widget-container' => 'color: red;',
],
```

它会生成包含该部件实例选择器的 CSS：

```css
.elementor-123 .elementor-element.elementor-element-1a2b3c4 .widget-container {
	color: red;
}
```

如果省略部件包装器，样式将应用于页面上所有 `.widget-container` 类。使用包装器后，样式将仅应用于该部件的 `.widget-container` 类。这本质上是 Elementor 为特定部件实例创建作用域样式的方式。

### 元素 ID

当选择器中使用元素 ID 变量时：

```php
'selectors' => [
	'#elementor-element-{{ID}}' => 'color: red;',
],
```

它会生成包含该部件实例 ID 的 CSS：

```css
#elementor-element-1a2b3c4 {
	color: red;
}
```

元素 ID 变量有助于创建唯一元素，但当部件在页面上有多个实例时，这会带来问题。这是因为 `id` 属性在页面上应该是唯一的。因此，我们不鼓励外部开发者使用此技术。它仅在非常特定的用例中被 Elementor 内部使用。

## 控件值到 CSS 值的转换

每个控件返回不同的值类型，有些返回字符串，有些返回数组。因此你需要熟悉[控件类型](src/editor-controls/control-types)，这将帮助你理解如何正确地将它们转换为 CSS 值。

### 数据控件

所有数据控件都返回 `string` 类型。要将用户选择的值应用到样式中，我们需要将控件值插入到选择器参数中：

```php
'selectors' => [
	'{{WRAPPER}} .widget-container' => 'color: {{VALUE}};',
],
```

### 单位控制

[滑块控件](src/editor-controls/control-slider) 返回一个包含尺寸和单位的 `array`（`[ 'size' => '', 'unit' => '' ]`），要在选择器参数中使用此用户数据：

```php
'selectors' => [
	'{{WRAPPER}} .widget-container' => 'width: {{SIZE}}{{UNIT}};',
],
```

### 尺寸控制

[尺寸控制](src/editor-controls/control-dimensions) 返回一个包含所有四个边和单位的 `array` (`[ 'top' => '', 'right' => '', 'bottom' => '', 'left' => '', 'unit' => '', 'isLinked' => '' ]`)，以便在 `selectors` 参数中使用用户数据：

```php
'selectors' => [
	'{{WRAPPER}} .widget-container' => 'margin: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
],
```

### URL 控件

[URL 控件](src/editor-controls/control-url) 返回一个包含 URL 和一些属性的 `数组` (`[ 'url' => '', 'is_external' => '', 'nofollow' => '', 'custom_attributes' => '' ]`)，以便在 `selectors` 参数中使用用户数据：

```php
'selectors' => [
	'{{WRAPPER}} .widget-container' => 'background-image: url( {{URL}} );',
],
```

### 媒体控制

[媒体控件](src/editor-controls/control-media) 返回一个包含媒体 ID 和 URL 的 `array` (`[ 'id' => '', 'url' => '' ]`)，以便在选择器参数中使用用户数据：

```php
'selectors' => [
	'{{WRAPPER}} .widget-container' => 'background-image: url( {{URL}} );',
],
```

### 多值控件

其他多值控件会返回不同的 `array` 类型，但我们不对这些控件应用 CSS，因为它们被视为内容控件而非样式控件。

## 来自其他控件的值

在某些较少见的情况下，您可能需要多个样式控件来创建单个 CSS 属性。对于这些情况，Elementor 提供了在值前添加控件名称前缀的功能。此方法提供了从其他控件提取数据的方式。

### 简单示例

一个简单的示例是 `aspect-ratio` 场景，我们需要使用两个[数字控件](src/editor-controls/control-number)来设置一个 CSS 声明：

```css
aspect-ratio: {{width}} / {{height}};
```

要实现这一点，你需要两个控件，以及一个利用这两个控件值的 `selectors` 参数：

```php{14-16}
$this->add_control(
	'aspect-ratio-width',
	[
		'label' => esc_html__( '宽高比宽度', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::NUMBER,
	]
);

$this->add_control(
	'aspect-ratio-height',
	[
		'label' => esc_html__( '宽高比高度', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::NUMBER,
		'selectors' => [
			'{{WRAPPER}} .custom-container img' => 'aspect-ratio: {{aspect-ratio-width.VALUE}} / {{aspect-ratio-height.VALUE}};'
		],
	]
);
```

### 复杂示例

一个更复杂的示例是包含单个角度、多种颜色和停止位置的 `linear-gradient()`：

```css
background-image: linear-gradient(
	{{angle}},
	{{color1}} {{position1}},
	{{color2}} {{position2}},
	{{color3}} {{position3}}
);
```

在这种情况下，我们将允许您自行实现此功能，以便您进行练习。
---
title: "选择器字典"
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

# 选择器字典

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

在某些情况下，您可能需要更新特定控件的值。但这样做可能会破坏现有网站，因为这些网站将旧值存储在数据库中。针对这些情况，Elementor 提供了一个字典，帮助开发者在代码使用前将旧值转换为新值。

## 选择器字典参数

使用 `selectors_dictionary` 参数将旧值替换为新值。

```php{6-9}
$this->add_control(
	'text-align',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SELECT,
		'selectors_dictionary' => [
			'old-value-1' => 'new-value-1',
			'old-value-2' => 'new-value-2',
		],
	]
);
```

## 选择器字典示例

### 使用选择控件的字典

让我们看看如何更新控件值，并将控件从"**物理 CSS 属性**"迁移到"[逻辑 CSS 属性](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties)"。我们希望将 `text-align: right|center|left;` 替换为 `text-align: start|center|end;`。

原始控件在数据库中保存了三个值之一 - `right`、`center` 或 `left`：

```php{8,12,16}
$this->add_control(
	'text-align',
	[
		'label' => esc_html__( 'Alignment', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::CHOOSE,
		'default' => 'center',
		'options' => [
			'left' => [
				'title' => esc_html__( 'Left', 'textdomain' ),
				'icon' => 'eicon-text-align-left',
			],
			'center' => [
				'title' => esc_html__( 'Center', 'textdomain' ),
				'icon' => 'eicon-text-align-center',
			],
			'right' => [
				'title' => esc_html__( 'Right', 'textdomain' ),
				'icon' => 'eicon-text-align-right',
			],
		],
		'selectors' => [
			'{{WRAPPER}} .some-class' => 'text-align: {{VALUE}};',
		],
	]
);
```

现在，我们希望将这些值替换为 `start`、`center` 或 `end`。但是，为了向后兼容，我们必须提供一个解决方案，考虑到数据库中保存的旧值。

我们可以使用 `selectors_dictionary` 来解决这个问题：

```php{8-11,16-19,21-24}
$this->add_control(
	'text-align',
	[
		'label' => esc_html__( 'Alignment', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::CHOOSE,
		'default' => 'center',
		'options' => [
			'end' => [
				'title' => esc_html__( 'End', 'textdomain' ),
				'icon' => 'eicon-text-align-' . ( is_rtl() ? 'right' : 'left' ),
			],
			'center' => [
				'title' => esc_html__( 'Center', 'textdomain' ),
				'icon' => 'eicon-text-align-center',
			],
			'start' => [
				'title' => esc_html__( 'Start', 'textdomain' ),
				'icon' => 'eicon-text-align-' . ( is_rtl() ? 'left' : 'right' ),
			],
		],
		'selectors_dictionary' => [
			'left' => is_rtl() ? 'end' : 'start',
			'right' => is_rtl() ? 'start' : 'end',
		],
		'selectors' => [
			'{{WRAPPER}} .some-class' => 'text-align: {{VALUE}};',
		],
	]
);
```

### 带选择控件的字典

让我们看看如何将 `selectors_dictionary` 与选择控件结合使用。在这个案例中，一个流行的插件曾使用前缀类来保存 `border-style` 值。该插件为每种边框样式类型定义了 5 个 CSS 类：

```php
$this->add_control(
	'border_style',
	[
		'label' => esc_html__( 'Border Style', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SELECT,
		'options' => [
			'' => esc_html__( 'Default', 'textdomain' ),
			'1' => esc_html__( 'None', 'textdomain' ),
			'2' => esc_html__( 'Solid', 'textdomain' ),
			'3' => esc_html__( 'Double', 'textdomain' ),
			'4' => esc_html__( 'Dotted', 'textdomain' ),
			'5' => esc_html__( 'Dashed', 'textdomain' ),
		],
		'prefix_class' => 'border-style-',
	]
);
```

为了解决这个问题，并移除所有不必要的 CSS 类，我们可以按如下方式使用 `selectors_dictionary`：

```php{14-20}
$this->add_control(
	'border_style',
	[
		'label' => esc_html__( 'Border Style', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SELECT,
		'options' => [
			'' => esc_html__( 'Default', 'textdomain' ),
			'1' => esc_html__( 'None', 'textdomain' ),
			'2' => esc_html__( 'Solid', 'textdomain' ),
			'3' => esc_html__( 'Double', 'textdomain' ),
			'4' => esc_html__( 'Dotted', 'textdomain' ),
			'5' => esc_html__( 'Dashed', 'textdomain' ),
		],
		'selectors_dictionary' => [
			'1' => 'none',
			'2' => 'solid',
			'3' => 'double',
			'4' => 'dotted',
			'5' => 'dashed',
		],
		'selectors' => [
			'{{WRAPPER}}' => 'border-style: {{VALUE}};',
		],
	]
);
```

在这种情况下，用 `selectors` 替换 `prefix_class` 效率更高。此外，我们不会破坏向后兼容性。`selectors_dictionary` 有助于将旧值转换为新值。

## 注意事项

必须牢记：`selectors_dictionary` 参数仅适用于返回简单 `string` 值的控件。它不适用于多值控件、单位控件、分组控件或中继器，这些控件都返回 `array` 值。
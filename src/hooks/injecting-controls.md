---
title: "注入控件"
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

# 注入控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 提供了一套特殊的钩子，允许开发者以编程方式将新控件注入到多种类型的元素中。您可以将新控件注入到所有元素、特定元素、Elementor 默认小部件以及其他插件开发者开发的小部件中。

共有八个可用的钩子供选择，其中四个钩子用于[将控件注入到所有元素中](#targeting-all-elements)，另外四个钩子用于[将控件注入到特定元素中](#targeting-specific-elements)。

## 定位所有元素

### 钩子详情

* **钩子类型：** 动作钩子
* **钩子名称：**
  * `elementor/element/before_section_start`
  * `elementor/element/after_section_start`
  * `elementor/element/before_section_end`
  * `elementor/element/after_section_end`
* **影响范围：** 编辑器

### Hook Arguments

| Argument     | Type                          | Description                                                   |
|--------------|-------------------------------|---------------------------------------------------------------|
| `element`    | _`\Elementor\Controls_Stack`_ | The edited element.                                           |
| `section_id` | _`string`_                    | Section id.                                                   |
| `args`       | _`array`_                     | Section arguments sent to `$element->start_controls_section`  |

### `elementor/element/before_section_start`

### `elementor/element/after_section_end`

在编辑器部分注册之前或之后运行。这用于在某个部分前后添加额外的部分，并影响面板中的所有元素。如果你需要在特定位置（特定元素和部分）添加一个部分，下面描述的钩子会更合适（参见“**定位特定元素**”部分）。

### Example

```php
/**
 * @param \Elementor\Controls_Stack $element    The element type.
 * @param string                    $section_id Section ID.
 * @param array                     $args       Section arguments.
 */
function inject_custom_control( $element, $section_id, $args ) {

	if ( 'section' === $element->get_name() && 'section_background' === $section_id ) {

		$element->start_controls_section(
			'custom_section',
			[
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
				'label' => esc_html__( 'Custom Section', 'textdomain' ),
			]
		);

		$element->add_control(
			'custom_control',
			[
				'type' => \Elementor\Controls_Manager::NUMBER,
				'label' => esc_html__( 'Custom Control', 'textdomain' ),
			]
		);

		$element->end_controls_section();

	}

}
add_action( 'elementor/element/before_section_start', 'inject_custom_control', 10, 3 );
```

### `elementor/element/after_section_start`

### `elementor/element/before_section_end`

在编辑器中某个部分打开后、关闭前运行。这是向现有部分添加额外控件的地方。如果您需要将控件添加到特定位置（特定元素和部分），下面描述的钩子会更合适。

### Example

```php
/**
 * @param \Elementor\Controls_Stack $element    The element type.
 * @param string                    $section_id Section ID.
 * @param array                     $args       Section arguments.
 */
function inject_custom_control( $element, $section_id, $args ) {

	if ( 'section' === $element->get_name() && 'section_background' === $section_id ) {

		$element->add_control(
			'custom_control',
			[
				'type' => \Elementor\Controls_Manager::NUMBER,
				'label' => esc_html__( 'Custom Control', 'textdomain' ),
			]
		);

	}

}
add_action( 'elementor/element/after_section_start', 'inject_custom_control', 10, 3 );
```

## 定位特定元素

### 钩子详情

* **钩子类型：** 动作钩子
* **钩子名称：**
  * `elementor/element/{$stack_name}/{$section_id}/before_section_start`
  * `elementor/element/{$stack_name}/{$section_id}/after_section_start`
  * `elementor/element/{$stack_name}/{$section_id}/before_section_end`
  * `elementor/element/{$stack_name}/{$section_id}/after_section_end`
* **说明：** 钩子名称中的动态部分 `$stack_name` 和 `$section_id` 分别指代栈名称和区块 ID。
* **影响范围：** 编辑器

要定位特定元素（如 `heading` 部件）和特定区块（如 `section_title` 区块），请使用以下钩子之一：
* `elementor/element/heading/section_title/before_section_start`
* `elementor/element/heading/section_title/after_section_start`
* `elementor/element/heading/section_title/before_section_end`
* `elementor/element/heading/section_title/after_section_end`

### Hook Arguments

| Argument  | Type             | Description                                                   |
|-----------|------------------|---------------------------------------------------------------|
| `element` | _`Element_Base`_ | The edited element.                                           |
| `args`    | _`array`_        | Section arguments sent to `$element->start_controls_section`. |

### `elementor/element/{$stack_name}/{$section_id}/before_section_start`

### `elementor/element/{$stack_name}/{$section_id}/after_section_end`

在特定元素和特定区块之前/之后运行。

### Example

```php
/**
 * @param \Elementor\Controls_Stack $element The element type.
 * @param array                     $args    Section arguments.
 */
function inject_heading_controls( $element, $args ) {

	$element->start_controls_section(
		'custom_section',
		[
			'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			'label' => esc_html__( 'Custom Section', 'textdomain' ),
		]
	);

	$element->add_control(
		'custom_control',
		[
			'type' => \Elementor\Controls_Manager::NUMBER,
			'label' => esc_html__( 'Custom Control', 'textdomain' ),
		]
	);

	$element->end_controls_section();

}
add_action( 'elementor/element/heading/section_title/before_section_start', 'inject_heading_controls', 10, 2 );
```

### `elementor/element/{$stack_name}/{$section_id}/after_section_start`

### `elementor/element/{$stack_name}/{$section_id}/before_section_end`

在编辑器部分内部运行，于其打开之后、关闭之前。这是在特定元素及其内部特定部分之前和之后添加额外控件的位置。

### Example

```php
/**
 * @param \Elementor\Controls_Stack $element The element type.
 * @param array                     $args    Section arguments.
 */
function inject_heading_controls( $element, $args ) {

	$element->add_control(
		'custom_control',
		[
			'type' => \Elementor\Controls_Manager::NUMBER,
			'label' => esc_html__( 'Custom Control', 'textdomain' ),
		]
	);

}
add_action( 'elementor/element/heading/section_title/before_section_start', 'inject_heading_controls', 10, 2 );
```
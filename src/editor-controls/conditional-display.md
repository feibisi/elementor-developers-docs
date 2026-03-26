---
title: "条件显示"
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

# 条件显示

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

在某些情况下，您可能需要根据用户在依赖控件中的选择来显示控件。例如，开启切换控件可能会触发其他控件的显示。编辑器中的控件机制具有特殊的条件显示功能。让我们看看如何使用它。

## 条件参数

要为 Elementor 控件设置条件显示，可在任何控件中使用 `condition` 参数。

### 单值条件

显示条件可能依赖于一个精确值：

```php{6-8}
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
		'condition' => [
			'dependent-control-name' => 'exact-value',
		],
	]
);
```

### 多值条件

显示条件可能依赖于一组值：

```php{6-8}
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
		'condition' => [
			'dependent-control-name' => [ 'value-1', 'value-2' ],
		],
	]
);
```

当传递一个值数组时，Elementor 使用逻辑 `OR` (`||`) 运算符。

## 多条件控制

显示条件可能依赖于多个控件。这就是为什么 `condition` 参数接受一个 `array`。它使用逻辑 `AND` (`&&`) 运算符，检查是否满足*所有*条件，以决定是否显示该控件。

要设置多个条件，请传递多个值：

```php{6-10}
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
		'condition' => [
			'dependent-control-1-name' => 'dependent-control-1-value',
			'dependent-control-2-name' => 'dependent-control-2-value',
			'dependent-control-3-name' => 'dependent-control-3-value',
		],
	]
);
```

## 相等运算符

条件语句包含两个相等运算符，可用于检查控制值是否*等于*或*不等于*某个值。

### 相等检查

仅当依赖控件等于特定值时显示控件：

```php
'condition' => [
	'control-name' => 'control-value',
],
```

### 不等条件检查

仅当依赖控件不等于特定值时显示控件：

```php
'condition' => [
	'control-name!' => 'control-value',
],
```

我们只需在控件名称后添加 `!` 后缀。

## 条件示例

让我们从一个示例开始，在这个示例中，我们希望允许用户设置边框并为其设置样式。为了简化用户体验，我们最初隐藏所有边框控件，只保留一个[切换器](src/editor-controls/control-switcher)。如果用户打开切换器，他们将看到所有边框控件。

```php{2,25-27,41-43,55-57}
$this->add_control(
	'border',
	[
		'label' => esc_html__( 'Border', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SWITCHER,
	]
);

$this->add_control(
	'border_style',
	[
		'label' => esc_html__( 'Border Style', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SELECT,
		'options' => [
			'' => esc_html__( 'None', 'textdomain' ),
			'solid' => esc_html__( 'Solid', 'textdomain' ),
			'double' => esc_html__( 'Double', 'textdomain' ),
			'dotted' => esc_html__( 'Dotted', 'textdomain' ),
			'dashed' => esc_html__( 'Dashed', 'textdomain' ),
			'groove' => esc_html__( 'Groove', 'textdomain' ),
		],
		'selectors' => [
			'{{WRAPPER}} .inner_class' => 'border-style: {{VALUE}}',
		],
		'condition' => [
			'border' => 'yes',
		],

	]
);

$this->add_control(
	'border_color',
	[
		'label' => esc_html__( 'Border Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'default' => '',
		'selectors' => [
			'{{WRAPPER}} .inner_class' => 'border-color: {{VALUE}}',
		],
		'condition' => [
			'border' => 'yes',
		],
	]
);

$this->add_responsive_control(
	'border_width',
	[
		'label' => esc_html__( 'Border Width', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::DIMENSIONS,
		'selectors' => [
			'{{WRAPPER}} .inner_class' => 'border-width: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
		],
		'condition' => [
			'border' => 'yes',
		],
	]
);
```

在上面的示例中，所有边框控件都依赖于单个边框控件。要设置多个依赖控件，我们可以设置更多条件，允许用户添加更多输入。

在下面的示例中，用户需要先打开切换器并设置边框样式。只有这样，颜色和宽度控件才会出现。为此，我们需要使用相等和不相等检查来设置多个条件。

```php{2,25-27,41-44,56-59}
$this->add_control(
	'border',
	[
		'label' => esc_html__( 'Border', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SWITCHER,
	]
);

$this->add_control(
	'border_style',
	[
		'label' => esc_html__( 'Border Style', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SELECT,
		'options' => [
			'' => esc_html__( 'None', 'textdomain' ),
			'solid' => esc_html__( 'Solid', 'textdomain' ),
			'double' => esc_html__( 'Double', 'textdomain' ),
			'dotted' => esc_html__( 'Dotted', 'textdomain' ),
			'dashed' => esc_html__( 'Dashed', 'textdomain' ),
			'groove' => esc_html__( 'Groove', 'textdomain' ),
		],
		'selectors' => [
			'{{WRAPPER}} .inner_class' => 'border-style: {{VALUE}}',
		],
		'condition' => [
			'border' => 'yes',
		],

	]
);

$this->add_control(
	'border_color',
	[
		'label' => esc_html__( '边框颜色', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'default' => '',
		'selectors' => [
			'{{WRAPPER}} .inner_class' => 'border-color: {{VALUE}}',
		],
		'condition' => [
			'border' => 'yes',
			'border_style!' => '',
		],
	]
);

$this->add_responsive_control(
	'border_width',
	[
		'label' => esc_html__( '边框宽度', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::DIMENSIONS,
		'selectors' => [
			'{{WRAPPER}} .inner_class' => 'border-width: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
		],
		'condition' => [
			'border' => 'yes',
			'border_style!' => '',
		],
	]
);

## 高级条件

Elementor 为编辑器中的控件提供了高级条件显示功能。请使用带 **s** 的 `conditions` 参数（而非 `condition` 参数）。

### 可用值

`conditions` 参数接受一个包含以下值的数组：

<table>
	<thead>
		<tr>
			<th>名称</th>
			<th>描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th><code>relation</code></th>
			<td>(<code>string</code>) 使用 <code>and</code> / <code>or</code> 逻辑运算符进行关系检查。<br> 默认值为 <code>and</code>。</td>
		</tr>
		<tr>
			<th><code>terms</code></th>
			<td>(<code>array</code>) 一个包含规则的数组的数组。
				<ul>
					<li><code>name</code> - 依赖控件的名称。</li>
					<li><code>value</code> - 依赖控件的值。</li>
					<li><code>operator</code> - 相等运算符，包括 <code>==</code>, <code>!=</code>, <code>!==</code>, <code>in</code>, <code>!in</code>, <code>contains</code>, <code>!contains</code>, <code><</code>, <code><=</code>, <code>></code>, <code>>=</code>, <code>===</code>。默认值为 <code>===</code>。</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

### More Operators

Before implementing the 'conditions' argument, you could only use equality and inequality checks. Now you have many more operators at your disposal: `==`, `!=`, `!==`, `in`, `!in`, `contains`, `!contains`, `<`, `<=`, `>`, `>=` and `===`.

We can replace the simple `condition` argument:

```php
'condition' => [
	'control-name!' => 'control-value',
],
```

with the advanced `conditions` argument, and include the `operator` rule inside the `term` array:

```php
'conditions' => [
	'terms' => [
		[
			'name' => 'control-name',
			'operator' => '!==',
			'value' => 'control-value',
		],
	],
],
```

This also makes it easier to use equality operators for numeric values (`<`, `<=`, `>`, `>=`, `==`, `===`, `!=` and `!==`):

```php
'conditions' => [
	'terms' => [
		[
			'name' => 'spacing',
			'operator' => '>=',
			'value' => 0,
		],
	],
],
```

Below is an example of checking against multiple values:

```php
'conditions' => [
	'terms' => [
		[
			'name' => 'background_type',
			'operator' => 'in',
			'value' => [ 'classic', 'gradient', 'video', 'slideshow' ],
		],
	],
],
```

Below is an example of checking if the term contains a value:

```php
'conditions' => [
	'terms' => [
		[
			'name' => 'heading',
			'operator' => 'contains',
			'value' => 'elementor',
		],
	],
],
```

### 多条件设置

如上所述，简单的 `condition` 参数允许开发者组合多个条件：

```php
'condition' => [
	'border' => 'yes',
	'border_style!' => '',
],
```

高级的 `conditions` 参数也具备相同能力：

```php
'conditions' => [
    'terms' => [
        [
            'name' => 'border',
            'operator' => '===',
            'value' => 'yes',
        ],
        [
            'name' => 'border_style',
            'operator' => '!==',
            'value' => '',
        ],
    ],
],
```

但使用 `condition` 参数时，必须满足所有条件才会显示控件；而高级的 `conditions` 参数则允许您通过新增的 `relation` 值来添加更多逻辑运算符。

### 条件关系

现在我们可以使用 `and` 逻辑运算符以及 `or` 运算符来检查条件之间的关系：

```php
'conditions' => [
	'relation' => 'or',
	'terms' => [
		[
			'name' => 'background',
			'operator' => '!==',
			'value' => '',
		],
		[
			'name' => 'border',
			'operator' => '!==',
			'value' => '',
		],
	],
],
```

### 嵌套条件

我们还可以嵌套条件：

```php
'conditions' => [
	'relation' => 'or',
	'terms' => [
		[
			'name' => 'video_type',
			'operator' => '===',
			'value' => 'youtube',
		],
		[
			'relation' => 'and',
			'terms' => [
				[
					'name' => 'show_image_overlay',
					'operator' => '===',
					'value' => 'yes',
				],
				[
					'name' => 'video_type',
					'operator' => '!==',
					'value' => 'hosted',
				],
			],
		],
	],
],
```

这一切使开发者能够创建具有许多嵌套级别的非常严格的规则，用于条件控制显示。

## 重复器与条件显示

条件控制显示和[重复器](src/editor-controls/control-repeater)属于特殊情况。有些操作可以实现，有些则不能。我们来探讨三种使用场景。

### 整个重复器控件

您可以有条件地隐藏/显示整个重复器：

```php{2,8-9,30-32}
$this->add_control(
	'display_list',
	[
		'label' => esc_html__( 'Display List', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SWITCHER,
		'label_on' => esc_html__( 'Yes', 'textdomain' ),
		'label_off' => esc_html__( 'No', 'textdomain' ),
		'return_value' => 'yes',
		'default' => 'yes',
	]
);

$this->add_control(
	'list',
	[
		'label' => esc_html__( 'Repeater List', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::REPEATER,
		'fields' => [
			[
				'name' => 'list_title',
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
			],
			[
				'name' => 'list_content',
				'label' => esc_html__( 'Content', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::WYSIWYG,
			],
		],
		'condition' => [
			'display_list' => 'yes',
		],
	]
);
```

在这种情况下有两个控件，第一个控件的值会影响第二个控件的显示。

### 中继器内部字段

您可以根据条件隐藏/显示中继器内部的字段：

```php{8,13-14,25-27}
$this->add_control(
	'list',
	[
		'label' => esc_html__( 'Repeater List', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::REPEATER,
		'fields' => [
			[
				'name' => 'display_content',
				'label' => esc_html__( 'Display Content', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::SWITCHER,
				'label_on' => esc_html__( 'Yes', 'textdomain' ),
				'label_off' => esc_html__( 'No', 'textdomain' ),
				'return_value' => 'yes',
				'default' => 'yes',
			],
			[
				'name' => 'list_title',
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
			],
			[
				'name' => 'list_content',
				'label' => esc_html__( 'Content', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::WYSIWYG,
				'condition' => [
					'display_content' => 'yes',
				],
			],
		],
	]
);
```

在此示例中，我们有一个包含三个内部控件的中继器，其中一个内部控件的值会影响另一个内部控件的显示。

### 不同层级的依赖关系

但是你不能混合不同的层级。内部控件不能依赖于主控件的值。

```php{2,8-9,28-30}
$this->add_control(
	'display_content',
	[
		'label' => esc_html__( 'Display Content', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::SWITCHER,
		'label_on' => esc_html__( 'Yes', 'textdomain' ),
		'label_off' => esc_html__( 'No', 'textdomain' ),
		'return_value' => 'yes',
		'default' => 'yes',
	]
);

$this->add_control(
	'list',
	[
		'label' => esc_html__( 'Repeater List', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::REPEATER,
		'fields' => [
			[
				'name' => 'list_title',
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
			],
			[
				'name' => 'list_content',
				'label' => esc_html__( 'Content', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::WYSIWYG,
				'condition' => [
					'display_content' => 'yes',
				],
			],
		],
	]
);
```

这是不允许的。它不会生效。
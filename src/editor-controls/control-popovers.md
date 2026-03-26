---
title: "控制项弹出框"
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

# 控制项弹出框

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

控制项弹出框是用于分组控制项并将其显示在面板上方弹出窗口中的 UI 包装器。使用弹出框可以帮助您通过将控制项移至弹出框来简化面板，仅当用户选择查看它们时才显示。一个很好的例子是排版控制项。它包含一个切换开关，只有当用户选择更改默认排版设置时，额外的控制项才会出现在弹出框中。弹出框使用两种方法创建：`start_popover()` 创建新弹出框，`end_popover()` 关闭弹出框。

## 控制项弹出框结构

使用以下代码添加新的控制项弹出框：

```php
$this->add_control(
	'popover-toggle',
	[
		'type' => \Elementor\Controls_Manager::POPOVER_TOGGLE,
		'label' => esc_html__( 'Box', 'textdomain' ),
		'label_off' => esc_html__( 'Default', 'textdomain' ),
		'label_on' => esc_html__( 'Custom', 'textdomain' ),
		'return_value' => 'yes',
	]
);

$this->start_popover();

$this->end_popover();
```

## 控制项参数

每个控制项具有以下关键参数：

* **弹出框名称** `(string)` – 代码中使用的唯一标识符。
* **弹出框设置** `(array)` – 额外的弹出框参数。
  * **标签** `(string)` – 在面板中向用户显示的标签。
  * **类型** `(string)` – 控制项类型。
  * **关闭标签** `(string)` – 设置默认设置时显示的标签。
  * **开启标签** `(string)` – 设置自定义设置时显示的标签。
  * **返回值** `(string)` – 设置自定义设置时返回的字符串。
  * **条件** `(array)` – 控制项显示条件。

## 示例

### 控制项弹出框

在下面的示例中，我们将控制项分组到两个弹出框中 - "正常" 选项卡和 "悬停" 选项卡：

```php {13-22,24,32}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style Section', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_control(
			'popover-toggle',
			[
				'label' => esc_html__( 'Box', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::POPOVER_TOGGLE,
				'label_off' => esc_html__( 'Default', 'textdomain' ),
				'label_on' => esc_html__( 'Custom', 'textdomain' ),
				'return_value' => 'yes',
			]
		);

		$this->start_popover();

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_popover();

		$this->end_controls_section();

	}

}
```
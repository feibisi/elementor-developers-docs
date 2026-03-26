---
title: "控制选项卡"
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

# 控制选项卡

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-tabs.png')" alt="Control Tabs" style="float: right;">

控制选项卡是用于在面板中排列区域和控件的 UI 包装器。控件必须添加到区域中，而区域是选项卡的一部分。选项卡使用两个方法创建：`start_controls_tabs()` 创建新选项卡，而 `end_controls_tabs()` 关闭选项卡。每个选项卡区域都有内部选项卡元素，这些内部选项卡也使用两个方法创建：`start_controls_tab()` 创建新的内部选项卡，而 `end_controls_tab()` 关闭内部选项卡。

## 控制选项卡结构

使用以下代码添加新的控制选项卡：

```php
$this->start_controls_tabs(
	'style_tabs'
);

$this->start_controls_tab(
	'style_normal_tab',
	[
		'label' => esc_html__( 'Normal', 'textdomain' ),
	]
);

$this->end_controls_tab();

$this->end_controls_tabs();
```

## 控制参数

每个*选项卡控制*具有以下关键参数：

* **选项卡名称** `(string)` – 代码中使用的唯一 ID。

每个*内部选项卡控制*具有以下关键参数：

* **选项卡名称** `(string)` – 代码中使用的唯一 ID。
* **选项卡设置** `(array)` – 额外的选项卡参数。
  * **标签** `(string)` – 在面板中向用户显示的标签。

## 示例

### 控制选项卡

让我们将控件分组到两个选项卡中 - "正常" 和 "悬停"：

```php {13-15,17-22,30,32-37,45,47}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style Section', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->start_controls_tabs(
			'style_tabs'
		);

		$this->start_controls_tab(
			'style_normal_tab',
			[
				'label' => esc_html__( 'Normal', 'textdomain' ),
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_tab();

		$this->start_controls_tab(
			'style_hover_tab',
			[
				'label' => esc_html__( 'Hover', 'textdomain' ),
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_tab();

		$this->end_controls_tabs();

		$this->end_controls_section();

	}

}
```
---
title: "控制项分组"
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

# 控制项分组

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-sections.png')" alt="Controls Section" style="float: right;">

控制项分组是用于在面板标签页下排列控制项的 UI 包装器。这些控制项被划分为多个分组，每个控制项必须属于一个分组。这些分组通过两种方法创建：`start_controls_section()` 用于创建新分组，而 `end_controls_section()` 用于关闭分组。

## 控制面板结构

按照以下步骤添加新的控制面板：

```php
$this->start_controls_section(
	'my_section',
	[
		'label' => esc_html__( '我的面板', 'textdomain' ),
		'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
	]
);

$this->end_controls_section();
```

## 控制参数

每个控件都包含以下关键参数：

* **区块名称** `(string)` – 在代码中使用的唯一标识符。
* **区块设置** `(array)` – 额外的区块参数。
  * **标签** `(string)` – 在面板中向用户显示的标签。
  * **标签页** `(string)` – 区块所在的标签页。默认为 `content`。
  * **条件** `(array)` – 控件的显示条件。

## 示例

### 单一部分

下面的示例创建了一个单独的部分，它将属于"**内容**"选项卡。我们需要提供部分名称以及额外参数，例如部分标签：

```php {5-11,19}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

	}

}
```

这将在"**内容**"选项卡下创建一个新的"**内容**"部分。

<img :src="$withBase('/assets/img/elementor-single-section.png')" alt="Elementor Single Section">

### 多个控制区域

现在让我们为"**内容**"选项卡创建多个控制区域：

```php {5-11,19,21-27,35}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

		$this->start_controls_section(
			'info_section',
			[
				'label' => esc_html__( 'Info', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

	}

}
```

这将在"**内容**"选项卡下为我们的控件创建两个区域。

<img :src="$withBase('/assets/img/elementor-multiple-sections.png')" alt="Elementor Multiple Sections">

### 多标签页中的区块

下一步是在"**内容**"标签页和"**样式**"标签页下创建新区块。这可以通过在额外参数数组中指定标签页名称来实现。

Elementor 提供了一个预定义的标签页列表供您使用，但对于小部件，惯例是仅使用"**内容**"标签页和"**样式**"标签页。

```php {5-11,19,21-27,35,37-43,51}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

		$this->start_controls_section(
			'info_section',
			[
				'label' => esc_html__( 'Info', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

	}

}
```

在此示例中，我们在"**内容**"标签页下创建了两个区块，并在"**样式**"标签页下创建了另一个区块。

<img :src="$withBase('/assets/img/elementor-section-in-a-tab.png')" alt="Elementor Section in a Tab">

从代码中可以看出，除非我们定义了"tab"参数，否则区块将默认添加到"**内容**"标签页。
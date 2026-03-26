---
title: "常规控件"
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

# 常规控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

常规控件是基础构建模块，允许用户为不同类型的输入字段（文本、数字、颜色、图像、图标等）设置不同的值。常规控件通过 `add_control()` 方法添加。

## 常规控件结构

使用以下代码添加控件：

```php
$this->add_control(
	'control-name',
	[
		'label' => esc_html__( '标题', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
	]
);
```

## 控制参数

每个控件包含以下关键参数：

* **控件名称** `(string)` – 代码中使用的唯一标识符。
* **控件设置** `(array)` – 额外的控制参数。每个控件除了基于控件类型的默认设置外，还有其专属的*自定义设置*。例如，文本控件有"占位符"设置，滑块有"范围"设置，颜色控件有"默认值"设置等。

## 示例

### 文本控件

在下面的示例中，我们将添加一个在 `control_text` 类中定义的简单文本控件，该控件允许用户保存一个简单的字符串。该控件将设置一个占位符：

```php {13-20}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'title',
			[
				'type' => \Elementor\Controls_Manager::TEXT,
				'label' => esc_html__( 'Title', 'textdomain' ),
				'placeholder' => esc_html__( 'Enter your title', 'textdomain' ),
			]
		);

		$this->end_controls_section();

	}

}
```

### 数字控件

在下面的示例中，我们将添加一个在 `Control_Number` 类中定义的简单数字控件，它将允许用户保存数字：

```php {13-24}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'size',
			[
				'type' => \Elementor\Controls_Manager::NUMBER,
				'label' => esc_html__( 'Size', 'textdomain' ),
				'placeholder' => '0',
				'min' => 0,
				'max' => 100,
				'step' => 1,
				'default' => 50,
			]
		);

		$this->end_controls_section();

	}

}
```

### 选择控件

另一个简单的例子是 `Control_Select` 类，它允许用户选择预定义的字段：

```php {13-25}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'open_lightbox',
			[
				'type' => \Elementor\Controls_Manager::SELECT,
				'label' => esc_html__( 'Lightbox', 'textdomain' ),
				'options' => [
					'default' => esc_html__( 'Default', 'textdomain' ),
					'yes' => esc_html__( 'Yes', 'textdomain' ),
					'no' => esc_html__( 'No', 'textdomain' ),
				],
				'default' => 'no',
			]
		);

		$this->end_controls_section();

	}

}
```

### 选择控件

选择控件是下拉选择控件的改进版本。`Control_Choose` 类允许用户选择预定义的字段，但每个选项的组件都带有图标样式。

```php {13-34}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'alignment',
			[
				'type' => \Elementor\Controls_Manager::CHOOSE,
				'label' => esc_html__( 'Alignment', 'textdomain' ),
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
				'default' => 'center',
			]
		);

		$this->end_controls_section();

	}

}
```

### 滑块控件

另一个有用的控件是 `Control_Slider`，它显示一个可拖动的范围滑块：

```php {13-30}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'font_size',
			[
				'type' => \Elementor\Controls_Manager::SLIDER,
				'label' => esc_html__( 'Size', 'textdomain' ),
				'size_units' => [ 'px', 'em', 'rem', 'custom' ],
				'range' => [
					'px' => [
						'min' => 1,
						'max' => 200,
					],
				],
				'default' => [
					'unit' => 'px',
					'size' => 20,
				],
			]
		);

		$this->end_controls_section();

	}

}
```

### 颜色控制

`Control_Color` 是较为流行的控件之一，它允许用户选择颜色：

```php {13-20}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'text_color',
			[
				'type' => \Elementor\Controls_Manager::COLOR,
				'label' => esc_html__( 'Text Color', 'textdomain' ),
				'default' => '#fefefe',
			]
		);

		$this->end_controls_section();

	}

}
```

### 媒体控件

最后，对于高级用户，您可以使用 `Control_Media` 从 WordPress 媒体库中选择图片：

```php {13-22}
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'image',
			[
				'type' => \Elementor\Controls_Manager::MEDIA,
				'label' => esc_html__( 'Choose Image', 'textdomain' ),
				'default' => [
					'url' => \Elementor\Utils::get_placeholder_image_src(),
				]
			]
		);

		$this->end_controls_section();

	}

}
```
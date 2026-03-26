---
title: "Widget Controls"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Widgets
    - Src
    - Repos
---

# Widget Controls

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Each widget needs to have some [controls](src/editor-controls) (setting fields), where users can select their data. This data is saved in the database and later used to [generate custom output](src/widgets/widget-rendering) based on the user's selection.

## 注册控件

在您的小部件类中，可以在 `register_controls()` 方法内添加控件，如下所示：

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section();

		$this->add_control();

		$this->add_control();

		$this->add_control();

		$this->end_controls_section();

	}

}
```

* **小部件控件** – `register_controls()` 方法允许您定义小部件将包含哪些控件（设置字段）。

## 可用控件

Elementor 提供了[多种现成控件](src/editor-controls/control-types)。所有控件必须包含在[章节](src/editor-controls/control-section)中。您可以添加[常规控件](src/editor-controls/regular-control)、[响应式控件](src/editor-controls/responsive-control)和[分组控件](src/editor-controls/group-control)。开发者甚至可以[创建新控件](src/controls)。

## Add Controls to your Widget

In the example below, we're going to add a few controls to a widget to allow users save data:

```php {13-20,22-33,35-47,49-70}
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
---
title: "动态标签控件"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Dynamic Tags
    - Src
    - Repos
---

# 动态标签控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

简单标签返回没有依赖关系的动态数据，例如随机数。更复杂的标签可能包含可选字段，用户可以在其中配置自定义数据，例如用户可以设置最小值和最大值的随机数。随后，渲染方法将使用这些自定义字段来生成最终输出。

## 注册控件

要为动态标签设置自定义控件，请使用 `register_controls()` 方法，如下所示：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	protected function register_controls(): void {

		$this->add_control(
			'text_param',
			[
				'type' => \Elementor\Controls_Manager::TEXT,
				'label' => esc_html__( 'Text Param', 'textdomain' ),
				'placeholder' => esc_html__( 'Enter your title', 'textdomain' ),
			]
		);

		$this->add_control(
			'number_param',
			[
				'type' => \Elementor\Controls_Manager::NUMBER,
				'label' => esc_html__( 'Number Param', 'textdomain' ),
				'min' => 0,
				'max' => 100,
				'step' => 1,
				'default' => 50,
			]
		);

		$this->add_control(
			'select_param',
			[
				'type' => \Elementor\Controls_Manager::SELECT,
				'label' => esc_html__( 'Select Param', 'textdomain' ),
				'options' => [
					'default' => esc_html__( 'Default', 'textdomain' ),
					'yes' => esc_html__( 'Yes', 'textdomain' ),
					'no' => esc_html__( 'No', 'textdomain' ),
				],
				'default' => 'no',
			]
		);

	}

}
```

相同的控件机制也用于[小部件控件](src/widgets/widget-controls)。
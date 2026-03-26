---
title: "文本阴影控制"
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

# 文本阴影控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 文本阴影控件显示用于水平阴影、垂直阴影、阴影模糊和阴影颜色的输入字段。

该控件在继承 `Control_Base_Multiple` 类的 `Control_Text_Shadow` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::TEXT_SHADOW` 常量。

## 参数


## 返回值

```
[
	'horizontal' => 0,
	'vertical' => 0,
	'blur' => 10,
	'color' => 'rgba(0,0,0,0.3)',
];
```

(_`array`_) 包含文本阴影数据的数组：

* **$horizontal** (_`int`_) 文本阴影水平大小。
* **$vertical** (_`int`_) 文本阴影垂直大小。
* **$blur** (_`int`_) 文本阴影模糊度。
* **$color** (_`string`_) 文本阴影颜色。

## 用法

```php {14-23}
<?php
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
			'custom_text_shadow',
			[
				'label' => esc_html__( 'Text Shadow', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT_SHADOW,
				'selectors' => [
					'{{SELECTOR}}' => 'text-shadow: {{HORIZONTAL}}px {{VERTICAL}}px {{BLUR}}px {{COLOR}};',
				],
			]
		);

		$this->end_controls_section();

	}

}
```

## 注意事项

请注意，开发者不应使用此控件，而应使用[文本阴影组控件](src/editor-controls/group-control-text-shadow)。
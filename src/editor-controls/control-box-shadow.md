---
title: "盒阴影控制"
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

# 盒阴影控制

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 盒阴影控制显示用于水平阴影、垂直阴影、阴影模糊、阴影扩散和阴影颜色的输入字段。

该控件在继承 `Control_Base_Multiple` 类的 `Control_Box_Shadow` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::BOX_SHADOW` 常量。

## 参数


## 返回值

```
[
	'horizontal' => 0,
	'vertical' => 0,
	'blur' => 10,
	'spread' => 0,
	'color' => 'rgba(0,0,0,0.5)',
]
```

(_`array`_) 包含盒阴影数据的数组：

* **$horizontal** (_`int`_) 盒阴影水平尺寸。
* **$vertical** (_`int`_) 盒阴影垂直尺寸。
* **$blur** (_`int`_) 盒阴影模糊度。
* **$spread** (_`int`_) 盒阴影扩散度。
* **$color** (_`string`_) 盒阴影颜色。

## 用法

```php {14-23}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'style_section',
			[
				'label' => esc_html__( 'Style', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_STYLE,
			]
		);

		$this->add_control(
			'custom_box_shadow',
			[
				'label' => esc_html__( 'Box Shadow', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::BOX_SHADOW,
				'selectors' => [
					'{{SELECTOR}}' => 'box-shadow: {{HORIZONTAL}}px {{VERTICAL}}px {{BLUR}}px {{SPREAD}}px {{COLOR}};',
				],
			]
		);

		$this->end_controls_section();

	}

}
```

## 注意事项

请注意，开发者不应使用此控件，而应使用[盒阴影组控制](src/editor-controls/group-control-box-shadow)。
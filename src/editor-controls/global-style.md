---
title: "全局样式"
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

# 全局样式

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 终端用户可通过[站点设置面板](src/editor/site-settings-panel)设置全局样式。编辑器中的控制机制具备特殊功能，允许用户设置自定义样式或继承全局样式。下面我们来看看如何设置。

## Global Argument

To set global styles with Elementor controls, use the `global` argument in any color or typography control:

```php{6-8}
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'global' => [
			// ...
		],
	]
);
```

<img :src="$withBase('/assets/img/elementor-global-style-indicator.png')" alt="Elementor Global Style Indicator" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

When setting a `global` argument for controls, the control has an additional globe icon which indicates to the end-user that they can either use one of the defined global styles or set a custom style.

## 可用全局样式

最终用户可在站点设置面板中定义网站的设计系统。Elementor 设计系统目前支持：

<img :src="$withBase('/assets/img/elementor-design-system.png')" alt="Elementor Design System" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

*   **全局颜色**
*   **全局字体**

Elementor 提供 4 种默认颜色和 4 套默认字体样式，用户可在此基础上添加自己的颜色和字体样式。

### 全局颜色

* `\Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_PRIMARY`
* `\Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_SECONDARY`
* `\Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_TEXT`
* `\Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_ACCENT`

### 全局字体

* `\Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_PRIMARY`
* `\Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_SECONDARY`
* `\Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_TEXT`
* `\Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_ACCENT`

## 全局示例

让我们看看控件如何从站点设计系统继承全局样式，这些样式在站点设置面板中定义：

```php{9-11,23-25,37-39,48-50,59-61,70-72}
$this->add_control(
	'heading_color',
	[
		'label' => esc_html__( 'Heading Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .heading-class' => 'color: {{VALUE}};',
		],
		'global' => [
			'default' => \Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_PRIMARY,
		],
	]
);

$this->add_control(
	'sub_heading_color',
	[
		'label' => esc_html__( 'Sub Heading Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .sub-heading-class' => 'color: {{VALUE}};',
		],
		'global' => [
			'default' => \Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_SECONDARY,
		],
	]
);

$this->add_control(
	'content_color',
	[
		'label' => esc_html__( 'Content Color', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::COLOR,
		'selectors' => [
			'{{WRAPPER}} .content-class' => 'color: {{VALUE}};',
		],
		'global' => [
			'default' => \Elementor\Core\Kits\Documents\Tabs\Global_Colors::COLOR_TEXT,
		],
	]
);

$this->add_group_control(
	\Elementor\Group_Control_Typography::get_type(),
	[
		'name' => 'heading_typography',
		'selector' => '{{WRAPPER}} .heading-class',
		'global' => [
			'default' => \Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_PRIMARY,
		],
	]
);

$this->add_group_control(
	\Elementor\Group_Control_Typography::get_type(),
	[
		'name' => 'sub_heading_typography',
		'selector' => '{{WRAPPER}} .sub_heading-class',
		'global' => [
			'default' => \Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_SECONDARY,
		],
	]
);

$this->add_group_control(
	\Elementor\Group_Control_Typography::get_type(),
	[
		'name' => 'content_typography',
		'selector' => '{{WRAPPER}} .content-class',
		'global' => [
			'default' => \Elementor\Core\Kits\Documents\Tabs\Global_Typography::TYPOGRAPHY_TEXT,
		],
	]
);
```

总之，您可以设置控件是否可以从站点设计系统继承全局样式，如果可以，它将继承哪种类型的样式（主要、次要、文本或强调色）。
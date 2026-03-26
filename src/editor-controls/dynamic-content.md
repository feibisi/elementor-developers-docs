---
title: "动态内容"
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

# 动态内容

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 可以使用[动态标签](src/dynamic-tags)替换控件输出，以编程方式生成内容。动态功能将静态控件转变为智能组件。这有助于用户将来自各种来源的定制化数据添加到他们的网站。让我们看看如何设置。

## 动态参数

使用 `dynamic` 参数通过 Elementor 控件设置动态标签：

```php{6-8}
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
		'dynamic' => [
			'active' => true,
		],
	]
);
```

<img :src="$withBase('/assets/img/elementor-dynamic-tag-indicator.png')" alt="Elementor Dynamic Tag Indicator" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

当控件支持动态标签时，会添加一个额外的图标，向用户表明他们可以用任何动态标签替换内容。

## 动态示例

让我们看看一个简单的控件如何变为动态：

```php{8-10,20-22,35-37,47-49,61-63}
$this->add_control(
	'heading',
	[
		'label' => esc_html__( 'Heading', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
		'placeholder' => esc_html__( 'Enter your heading', 'textdomain' ),
		'label_block' => true,
		'dynamic' => [
			'active' => true,
		],
	]
);

$this->add_control(
	'content',
	[
		'label' => esc_html__( 'Content', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXTAREA,
		'placeholder' => esc_html__( 'Enter your content', 'textdomain' ),
		'dynamic' => [
			'active' => true,
		],
	]
);

$this->add_control(
	'count',
	[
		'label' => esc_html__( 'Count', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::NUMBER,
		'default' => 0,
		'min' => 0,
		'max' => 100,
		'step' => 1,
		'dynamic' => [
			'active' => true,
		],
	]
);

$this->add_control(
	'url',
	[
		'label' => esc_html__( 'Link', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::URL,
		'placeholder' => esc_html__( 'https://your-link.com', 'textdomain' ),
		'dynamic' => [
			'active' => true,
		],
	]
);

$this->add_control(
	'image',
	[
		'label' => esc_html__( 'Choose Image', 'elementor' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'default' => [
			'url' => \Elementor\Utils::get_placeholder_image_src(),
		],
		'dynamic' => [
			'active' => true,
		],
	]
);
```
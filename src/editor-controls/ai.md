---
title: "AI"
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

# AI

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

<img :src="$withBase('/assets/img/elementor-control-ai-button.png')" alt="Control AI Button" style="float: right;">

Elementor 已在众多控件中集成了 AI 功能，旨在赋能用户通过生成原创或增强的文本以及自定义代码（HTML 和 CSS）来提升其网站品质，从而帮助网页创作者提高工作效率。插件开发者可以选择启用或禁用 AI 按钮。若启用，他们可以控制 AI 功能。

## AI 功能

Elementor 的 AI 解决方案允许用户在编辑体验中生成新内容或更新现有内容。点击 AI 按钮将显示一个新对话框，用户可输入提示词来创建 AI 生成的内容。随后，用户可选择将内容添加到应用了 AI 的控件中，或对其进行调整，例如加长、缩短、改变语气等。

## 支持的控件

并非所有编辑器控件都支持 AI 功能，例如切换器控件和选择控件就没有 AI 按钮。但基于文本的控件、代码控件和媒体控件都新增了 AI 按钮。

以下控件默认带有 AI 按钮：

* [使用 AI 撰写](#write-with-ai)
  * [文本控件](src/editor-controls/control-text)
  * [文本区域控件](src/editor-controls/control-textarea)
  * [所见即所得控件](src/editor-controls/control-wysiwyg)
* [使用 AI 编写代码](#code-with-ai)
  * [代码控件](src/editor-controls/control-code)
* [使用 AI 创建](#create-with-ai)
  * [媒体控件](src/editor-controls/control-media)

在某些情况下，您可能不希望支持的控件上显示 AI 按钮，可以选择禁用 AI 按钮。例如，在允许用户设置元素 ID 的文本控件上添加 AI 按钮就没有意义。您可以禁用 AI 按钮。

也可能存在相反的情况：控件默认没有 AI 按钮，但您希望添加一个。例如，当[创建新的 Elementor 控件](src/controls)时，如果自定义功能包含文本区域，并且您希望允许网站创建者插入 AI 生成的内容，您可以添加 AI 按钮。

此外，每种控件类型会触发不同的提示选项和建议。文本控件主要用于生成短标题或较长段落，代码建议用于生成 HTML 和 CSS 代码，而媒体控件则用于生成图像。

## AI Argument

To manage AI capabilities for Elementor controls, use the `ai` argument. It’s an array that accepts the following options:

| Name       | Description |
|------------| ----------- |
| `active`   | (`boolean`) Whether to display the AI button to the control, or not. |
| `type`     | (`string`) The type of the control and the AI prompt options. Available values are: `text`, `textarea`, `code` and `media`. |
| `language` | (`string`) Override code control language. Available values are: `html` and `css`. |

## 使用方法

让我们通过几个实际示例，了解如何使用 Elementor AI 按钮来增强编辑器控件。

### 使用 AI 撰写

基于文本控件的 AI 功能：

```php
// 带有 AI 按钮的文本控件，用于生成短文本
$this->add_control(
	'title',
	[
		'label' => esc_html__( '标题', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
	]
);

// 带有 AI 按钮的文本区域控件，用于生成段落
$this->add_control(
	'description',
	[
		'label' => esc_html__( '描述', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXTAREA,
	]
);

// 带有 AI 按钮的 WYSIWYG 控件，用于生成段落
$this->add_control(
	'content',
	[
		'label' => esc_html__( '内容', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::WYSIWYG,
	]
);

// 带有 AI 按钮的文本区域控件，用于生成短文本
$this->add_control(
	'subheading',
	[
		'label' => esc_html__( '副标题', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXTAREA,
		'ai' => [
			'type' => 'text',
		],
	]
);

// 不带 AI 按钮的文本控件
$this->add_control(
	'title-id',
	[
		'label' => esc_html__( '标题 ID', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::TEXT,
		'ai' => [
			'active' => false,
		],
	]
);

// 为自定义控件添加 AI 按钮
$this->add_control(
	'unique-control-name',
	[
		'label' => esc_html__( '自定义元素', 'textdomain' ),
		'type' => \My_Addon::CUSTUM_TEXT_CONTROL,
		'ai' => [
			'active' => true,
			'type' => 'text',
		],
	]
);
```

### Code with AI

AI capabilities that generates custom code:

```php
// Code control with an AI button that generates CSS
$this->add_control(
	'custom-css',
	[
		'label' => esc_html__( 'Custom CSS', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::CODE,
		'language' => 'css',
	]
);

// Code control with an AI button that generates HTML
$this->add_control(
	'custom-html',
	[
		'label' => esc_html__( 'Custom HTML', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::CODE,
		'language' => 'html',
	]
);

// Code control without an AI button
$this->add_control(
	'css',
	[
		'label' => esc_html__( 'CSS', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::CODE,
		'language' => 'css',
		'ai' => [
			'active' => false,
		],
	]
);

// Override control language for AI
$this->add_control(
	'html',
	[
		'label' => esc_html__( 'HTML', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::CODE,
		'language' => 'html',
		'ai' => [
			'language' => 'css',
		],
	]
);
```

### Create with AI

AI capabilities on media controls:

```php
// Media control without an AI button
$this->add_control(
	'background-image',
	[
		'label' => esc_html__( 'Choose Image', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'ai' => [
			'active' => true,
		],

	]
);

// Media control with an AI button that generates background images
$this->add_control(
	'background-image',
	[
		'label' => esc_html__( 'Choose Image', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'dynamic' => [
			'active' => true,
		],
		'ai' => [
			'category' => 'background',
		],

	]
);

// Media control with an AI button that generates 3D images
$this->add_control(
	'3d-cover-image',
	[
		'label' => esc_html__( 'Choose Image', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'dynamic' => [
			'active' => true,
		],
		'ai' => [
			'category' => '3d',
		],

	]
);

// Media control with an AI button that generates photographic images
$this->add_control(
	'photo',
	[
		'label' => esc_html__( 'Choose Image', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'dynamic' => [
			'active' => true,
		],
		'ai' => [
			'category' => 'photographic',
		],

	]
);

// Media control with an AI button that generates handmade images
$this->add_control(
	'drawings',
	[
		'label' => esc_html__( 'Choose Image', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'dynamic' => [
			'active' => true,
		],
		'ai' => [
			'category' => 'handmade',
		],

	]
);

// Media control with an AI button that generates digital art
$this->add_control(
	'art-image',
	[
		'label' => esc_html__( 'Choose Image', 'textdomain' ),
		'type' => \Elementor\Controls_Manager::MEDIA,
		'dynamic' => [
			'active' => true,
		],
		'ai' => [
			'category' => 'digital-art',
		],

	]
);
```

**Note**: Non-image [media types](src/editor-controls/control-media#arguments) won't display the AI button as they are not supported.
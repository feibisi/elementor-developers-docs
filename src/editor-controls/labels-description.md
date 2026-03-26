---
title: "标签与描述"
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

# 标签与描述

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

控件本质上是供用户填写数据的输入字段。每个控件可包含显示在字段上方的标签，以及显示在字段下方的简短描述。编辑器中的控件机制提供特殊参数，帮助开发者设置这些字段并为其定义样式。

## 基本参数

编辑器中的每个控件都接受以下参数：

```php{5-6}
$this->add_control(
	'unique-control-name',
	[
		'type' => \Elementor\Controls_Manager::TEXT,
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'description' => esc_html__( 'Short control description.', 'textdomain' ),
		'show_label' => false,
		'label_block' => false,
		'separator' => 'after'
	]
);
```

| 名称          | 描述 |
|---------------| ----------- |
| `type`        | (`string`) 控件的类型。 |
| `label`       | (`string`) 显示在字段前/上方的标签。 |
| `description` | (`string`) 显示在字段下方的描述。 |
| `show_label`  | (`bool`)   是否显示标签。默认值为 `true`。 |
| `label_block` | (`bool`)   是否将标签显示在单独一行。默认值为 `false`。 |
| `separator`   | (`string`) 设置控件分隔符的位置。可用值有： <ul><li> `default` 将根据控件类型定位分隔符。</li><li> `before` / `after` 将在控件之前/之后定位分隔符。</li><li> `none` 将隐藏分隔符。</li></ul> 默认值为 `default`。 |

### 标签

<img :src="$withBase('/assets/img/controls/control-field-label.png')" alt="Elementor Control - Label View" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

控件标签代表编辑器中的字段标题。它是一个字符串，帮助用户理解控件代表什么。它也有助于使用屏幕阅读器或其他辅助技术的人。

```php{5}
$this->add_control(
	'unique-control-name',
	[
		'type' => \Elementor\Controls_Manager::TEXT,
		'label' => esc_html__( 'Control Label', 'textdomain' ),
	]
);
```

### 标签块

<img :src="$withBase('/assets/img/controls/control-field-label-block.png')" alt="Elementor Control - Label Block" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

控件的标签和输入字段并排显示在同一行。开发者可以选择以不同的方式设置控件样式，将它们上下堆叠，而不是并排显示。

```php{6}
$this->add_control(
	'unique-control-name',
	[
		'type' => \Elementor\Controls_Manager::TEXT,
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'label_block' => true,
	]
);
```

### Show Label

<img :src="$withBase('/assets/img/controls/control-field-label-hidden.png')" alt="Elementor Control - Hidden Label" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

By default all control labels are displayed in the editor. Developers can choose to hide label, leaving only the input field. Please note, for accessibility reasons, the label is not removed, it's only visually hidden.

```php{6}
$this->add_control(
	'unique-control-name',
	[
		'type' => \Elementor\Controls_Manager::TEXT,
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'show_label' => false,
	]
);
```

### 描述

<img :src="$withBase('/assets/img/controls/control-field-description.png')" alt="Elementor Control - Field Description" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

控件描述是显示在字段下方的简单文本，为用户提供关于该控件的更多信息。无论标签和字段是显示在同一行还是上下堆叠，描述都会显示在单独的一行。

```php{6}
$this->add_control(
	'unique-control-name',
	[
		'type' => \Elementor\Controls_Manager::TEXT,
		'label' => esc_html__( 'Control Label', 'textdomain' ),
		'description' => esc_html__( 'Short control description.', 'textdomain' ),
	]
);
```

### 分隔符

设置控件分隔符的位置。可用值包括：

* `default`：根据控件类型自动定位分隔符
* `before` / `after`：将分隔符置于控件前/后
* `none`：隐藏分隔符

此参数适用于在两个或更多控件之间进行分隔的场景。
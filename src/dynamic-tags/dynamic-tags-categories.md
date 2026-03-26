---
title: "动态标签分类"
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

# 动态标签分类

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

创建控件时，开发者可以定义[控件是否接受动态数据](src/editor-controls/dynamic-content)。若控件接受动态数据，则必须设置数据类型（如文本值、颜色、图像）。而动态标签需要定义其向控件返回的数据类型。

这正是分类发挥作用之处。Elementor Pro 提供按数据类型排列的分类列表，动态标签通过这些分类向控件返回数据。

## 可用分类常量

Elementor Pro 提供以下预定义的动态标签分类常量：

| 常量                 | 值          | 说明                                 |
|----------------------|-------------|--------------------------------------|
| `NUMBER_CATEGORY`    | `number`    | 用于数字控件的动态标签               |
| `TEXT_CATEGORY`      | `text`      | 用于文本控件的动态标签               |
| `URL_CATEGORY`       | `url`       | 用于 URL 控件的动态标签              |
| `COLOR_CATEGORY`     | `color`     | 用于颜色控件的动态标签               |
| `IMAGE_CATEGORY`     | `image`     | 用于图像控件的动态标签               |
| `MEDIA_CATEGORY`     | `media`     | 用于媒体控件的动态标签               |
| `GALLERY_CATEGORY`   | `gallery`   | 用于图库控件的动态标签               |
| `POST_META_CATEGORY` | `post_meta` | 用于文章元数据控件的动态标签         |

::: warning 请注意
在旧版 Elementor 中，您可以将返回值定义为简单文本，如 `url`、`number`、`text`、`media` 等。随着 Elementor 的发展，它已将这些基于文本的值替换为预定义的大写`常量`。我们强烈建议您将旧的文本基值替换为新的分类常量。
:::

## 在动态标签上应用分类

创建新的动态标签时，您需要定义该标签将返回的数据类型。这通过 `get_categories()` 方法实现：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function get_categories(): array {
		return [ \Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY ];
	}

}
```

该方法返回一个数组，意味着动态标签可以向控件返回多种数据类型：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function get_categories(): array {
		return [
			\Elementor\Modules\DynamicTags\Module::URL_CATEGORY,
			\Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY,
			\Elementor\Modules\DynamicTags\Module::NUMBER_CATEGORY
		];
	}

}
```

## 在控件中使用动态分类

另一方面，当您创建[控件](src/editor-controls)时，需要通过 `get_default_settings()` 方法在定义[控件设置](src/controls/control-settings)时支持动态标签，并选择要显示的分类：

```php {13-19}
class Elementor_Test_Control extends \Elementor\Base_Control {

	public function get_type(): string {}

	public function content_template(): void {}

	protected function get_default_settings(): array {

		return [
			'show_label' => true,
			'label_block' => true,
			'separator' => 'after',
			'dynamic' => [
				'active' => true,
				'categories' => [
					\Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY,
					\Elementor\Modules\DynamicTags\Module::NUMBER_CATEGORY
				],
			],
		];

	}

}
```
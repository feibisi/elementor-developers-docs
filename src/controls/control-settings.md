---
title: "控件设置"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Controls
    - Src
    - Repos
---

# 控件设置

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

**控件设置**允许开发者为控件设置默认值，例如标签、描述、是否显示分隔符、隐藏标签等。

## 可用设置

每个控件都有默认设置，这些设置决定了控件在面板中的结构和设计。这些默认设置在 `$_base_settings` 属性中定义。以下是所有控件共有的默认设置列表：

| 名称           | 类型         | 默认值     | 描述                                                                 |
|----------------|--------------|------------|----------------------------------------------------------------------|
| `label`        | _`string`_   |            | 显示在字段上方的标签                                                  |
| `description`  | _`string`_   |            | 显示在字段下方的描述                                                  |
| `show_label`   | _`bool`_     | `true`     | 是否显示标签                                                          |
| `label_block`  | _`bool`_     | `false`    | 是否在单独一行显示标签                                                |
| `separator`    | _`string`_   | `default`  | 设置控件分隔符的位置。可用值为 `default`、`before` 和 `after`。`default` 将隐藏分隔符，除非控件类型有特定的分隔符设置。`before` / `after` 会将分隔符定位在控件之前/之后。 |

每个控件都可以覆盖默认设置并添加新的自定义设置。

## 设置方法

如果控件使用默认设置，则无需将其添加到类中。如果要更改默认设置或添加新设置，请使用 `get_default_settings()` 方法。此方法应返回一个数组：

```php
class Elementor_Test_Control extends \Elementor\Base_Control {

	protected function get_default_settings(): array {

		return [
			'label_block' => true,
			'separator' => 'after',
			'new_settings_value' => '',
			'new_multiple_values' => [],
		];

	}

}
```

之后，在生成[控件模板](src/controls/control-template)时，可以利用这些设置。
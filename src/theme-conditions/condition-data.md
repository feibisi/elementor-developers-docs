---
title: "条件数据"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Theme Conditions
    - Src
    - Repos
---

# 条件数据

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

每个条件都包含基本信息，例如条件的唯一 ID 和条件标签。这些数据在代码中使用，并在编辑器中显示给用户。

## 数据方法

条件数据需要通过特定方法"返回"。这些方法很简单：

```php
class Elementor_Test_Condition extends \ElementorPro\Modules\ThemeBuilder\Conditions\Condition_Base {

	public function get_name(): string {
		return 'condition_name';
	}

	public function get_label(): string {
		return esc_html__( 'My Condition Name', 'textdomain' );
	}

}
```

* **条件类型** – `get_type()` 方法返回将在代码中使用的条件名称（ID）。

* **条件名称** – `get_name()` 方法返回将显示给用户的条件标签。
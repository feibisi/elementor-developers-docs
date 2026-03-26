---
title: "Action Data"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Form Actions
    - Src
    - Repos
---

# Action Data

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

每个操作都包含基本信息，例如唯一的操作 ID 和标签。这些数据在代码中使用，并在编辑器中显示给用户。

## 数据方法

操作数据需要通过特定方法“返回”。这些方法很简单：

```php
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function get_name(): string {
		return 'action_name';
	}

	public function get_label(): string {
		return esc_html__( 'My Action Name', 'textdomain' );
	}

}
```

* **操作名称** - `get_name()` 方法返回操作名称（ID），它将在代码中使用。

* **操作标签** - `get_label()` 方法返回操作标签，它将在编辑器中显示给用户。
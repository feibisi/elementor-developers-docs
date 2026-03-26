---
title: "动态标签数据"
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

# 动态标签数据

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

每个动态标签都需要基本信息，例如唯一 ID、标题、组别和类别。

## 数据方法

动态标签数据通过这些方法"返回"：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function get_name(): string {
		return 'tag-name';
	}

	public function get_title(): string {
		return esc_html__( 'Dynamic Tag Name', 'textdomain' );
	}

	public function get_group(): array {
		return [ 'group-name' ];
	}

	public function get_categories(): array {
		return [ \Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY ];
	}

}
```

* **动态标签名称** - `get_name()` 方法返回一个在代码中使用的唯一 ID。

* **动态标签标题** – `get_title()` 方法返回向用户显示的标签标签。

* **动态标签组别** – `get_group()` 方法返回标签将出现在其下的组别数组。

* **动态标签类别** – `get_categories()` 方法返回标签所属的控制类别数组。
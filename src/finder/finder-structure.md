---
title: "Finder 结构"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Finder
    - Src
    - Repos
---

# Finder 结构

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Finder 按类别组织，每个类别包含一组链接。

## Finder 类

要编辑 Finder 的类别，我们首先需要创建一个继承 `\Elementor\Core\Common\Modules\Finder\Base_Category` 类（基础 Finder 类别类）的类：

```php
class New_Finder_Category extends \Elementor\Core\Common\Modules\Finder\Base_Category {
}
```

## Finder 方法

扩展类将包含以下方法：

```php
class New_Finder_Category extends \Elementor\Core\Common\Modules\Finder\Base_Category {

	public function get_id(): string {}

	public function get_title(): string {}

	public function get_category_items(): array {}

	public function is_dynamic(): bool {}

}
```

* **类别 ID** - `get_id()` 方法返回一个在代码中使用的唯一 ID。

* **类别标题** - `get_title()` 方法返回向用户显示的标签。

* **类别项** - `get_category_items()` 方法返回属于该类别的链接数组。

* **是否为动态** - `is_dynamic()` 方法是一个可选方法，返回布尔值。当类别项通过 Ajax 请求（如文章/页面标题）返回数据时使用。本文档不涵盖此方法。
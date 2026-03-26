---
title: "控制结构"
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

# 控制结构

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

创建自定义控件是专为非常熟悉代码库的高级 Elementor 开发者保留的任务。这个过程从学习 `Base_Control` 类及其内部方法开始。这将使您能够理解 Elementor 如何创建不同的控件，以及如何自定义这些基础方法。

每个控件必须有两个基本方法——一个唯一的名称和在编辑器中显示字段的 HTML 代码。更高级的控件可以设置自定义设置、定义默认值、加载脚本和样式等等。

## 扩展控件

要创建您自己的控件，您需要**扩展**抽象基础控件：

```php
class Elementor_Test_Control extends \Elementor\Base_Control {
}
```

您也可以扩展[特定控件类型](src/editor-controls/control-types)之一：

```php
class Elementor_Test_Control extends \Elementor\Base_Data_Control {
}
```

这样，您的类将继承您所扩展类的所有方法。

## 控件方法

一个简单的控件只需要两个方法：控件类型和模板：

```php
class Elementor_Test_Control extends \Elementor\Base_Control {

	public function get_type(): string {}

	public function content_template(): void {}

}
```

更高级的控件可以使用其他可用方法：

```php
class Elementor_Test_Control extends \Elementor\Base_Control {

	public function get_type(): string {}

	protected function get_default_settings(): array {}

	public function get_default_value(): string {}

	public function content_template(): void {}

	public function enqueue(): void {}

}
```

这些方法可以分为以下几组：

* [设置](src/controls/control-settings)
* [模板](src/controls/control-template)
* [值](src/controls/control-values)
* [加载](src/controls/control-enqueue)
---
title: "使用控件"
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

# 使用控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

控件可以在 Elementor 小部件或 Elementor 面板中使用。最终用户使用控件来选择他们的数据。这些数据保存在数据库中，随后用于根据用户的选择生成自定义输出。

## 注册控件

在您的小部件类中，可以在 `register_controls()` 方法内添加控件，如下所示：

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section();

		$this->add_control();

		$this->add_responsive_control();

		$this->add_group_control();

		$this->end_controls_section();

	}

}
```

## 可用的控件类型

Elementor 有三种可以添加到小部件的**控件类型**：

* [常规控件](src/editor-controls/regular-control) – 添加单个控件。
* [响应式控件](src/editor-controls/responsive-control) – 添加一个可为不同屏幕尺寸设置不同值的控件。
* [组控件](src/editor-controls/group-control) – 添加一个将其他几个控件组合在一起的控件。

Elementor 还有**控件的 UI 包装器**，可用于对控件进行分组和重新排列：

* [控件部分](src/editor-controls/control-section) – 控件的包装器。
* [控件弹出框](src/editor-controls/control-popovers) – 切换弹出框控件的包装器。
* [控件选项卡](src/editor-controls/control-tabs) – 在选项卡中排列控件的包装器。

## 控件方法

Elementor 控件有一个用于注册设置字段的*单一方法*。控件的 UI 包装器有*两个/四个方法*来包装其他控件。

可用的方法：

* **常规控件** - `add_control()`
* **响应式控件** - `add_responsive_control()`
* **组控件** - `add_group_control()`
* **控件部分** - `start_controls_section()` 和 `end_controls_section()`
* **控件弹出框** - `start_popover()` 和 `end_popover()`
* **控件选项卡** - `start_controls_tabs()` 和 `end_controls_tabs()` 以及 `start_controls_tab()` 和 `end_controls_tab()`
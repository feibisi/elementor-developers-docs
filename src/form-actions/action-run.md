---
title: "Action Run"
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

# Action Run

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

表单提交时执行操作的实际方法。这是操作触发的主要方法。它可以使用来自自定义控件的可选数据，但这不是必需的。

## Run 方法

触发操作的方法称为 `run()`。该方法仅在表单提交时执行。在你的操作类中，按如下方式使用该方法：

```php
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function run( $record, $ajax_handler ): void {

		// ...

	}

}
```

*   **运行操作** - `run()` 方法在表单提交时触发实际的操作。`$record` 参数是一个表单记录实例，`$ajax_handler` 是表单 ajax 处理程序的实例。

## 执行操作

开发者可以在表单提交时执行任何代码，可能性是无限的。让我们看一些例子。

### 发送电子邮件

在下面的例子中，我们将在每次表单提交时发送一封电子邮件：

```php
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function run( $record, $ajax_handler ): void {

		wp_mail( /* ... */ );

	}

}
```

### 发送 HTTP 请求

在下面的例子中，我们将在每次表单提交时发送一个 HTTP 请求：

```php
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function run( $record, $ajax_handler ): void {

		wp_remote_post( /* ... */ )

	}

}
```

### 创建 WordPress 文章/页面/自定义文章类型

另一个用例是在每次表单提交后创建 WordPress 自定义文章类型：

```php
class Elementor_Test_Action extends \ElementorPro\Modules\Forms\Classes\Action_Base {

	public function run( $record, $ajax_handler ): void {

		wp_insert_post( /* ... */ );

	}

}
```
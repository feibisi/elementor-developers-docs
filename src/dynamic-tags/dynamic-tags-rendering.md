---
title: "动态标签渲染"
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

# 动态标签渲染

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

render 方法生成最终输出并将数据回显到控件。如果动态标签有控件，渲染函数应在生成输出时使用这些数据。

## 渲染方法

要渲染动态标签输出并回显数据，我们使用 `render()` 方法，如下所示：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function render(): void {

		echo rand();

	}

}
```

要从[动态标签控件](src/dynamic-tags/dynamic-tags-controls)中提取数据，我们可以使用 `get_settings()` 方法：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function render(): void {
		$param1 = $this->get_settings( 'text_param' );
		$param2 = $this->get_settings( 'number_param' );
		$param3 = $this->get_settings( 'select_param' );

		echo "{$param1} {$param2} {$param3}";
	}

}
```
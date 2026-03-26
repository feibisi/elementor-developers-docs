---
title: "动态标签结构"
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

# 动态标签结构

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

每个动态标签都需要具备一些基本设置，例如唯一的名称。除此之外，还有一些高级设置，如动态标签控件，这些基本上是可选字段，用户可以在其中配置自定义数据。还有一个渲染方法，它根据从动态标签控件获取的用户设置生成最终输出。

## 扩展动态标签

要创建自己的控件，您需要**扩展**动态标签控件以继承其方法：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {
}
```

## 动态标签方法

一个简单的动态标签骨架如下所示：

```php
class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function get_name(): string {}

	public function get_title(): string {}

	public function get_group(): array {}

	public function get_categories(): array {}

	protected function register_controls(): void {}

	public function render(): void {}

}
```

动态标签方法可以分为以下几组：

* [数据](src/dynamic-tags/dynamic-tags-data)
* [分组](src/dynamic-tags/dynamic-tags-groups)
* [类别](src/dynamic-tags/dynamic-tags-categories)
* [控件](src/dynamic-tags/dynamic-tags-controls)
* [渲染](src/dynamic-tags/dynamic-tags-rendering)

请注意，`\Elementor\Core\DynamicTags\Tag` 类还有许多其他方法，但上述方法将满足您的绝大部分需求。
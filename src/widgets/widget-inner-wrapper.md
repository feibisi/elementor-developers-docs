---
title: "Widget DOM Optimization"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Widgets
    - Src
    - Repos
---

# Widget DOM Optimization

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor widgets define their own markup in the `render()` method. However, Elementor wraps each widget in two `<div>` elements; the outer `<div class="elementor-widget">` element, and the inner `<div class="elementor-widget-container">` element. In the past, these additional wrappers allow Elementor to add additional styles and features.

However, two wrappers for each widget increases the overall DOM size, reducing page performance. To overcome this, developers can use the `has_widget_inner_wrapper()` method to control the number of wrapper elements the widget has.

By switching to a single wrapper, a widget can reduce the DOM size and optimize its footprint on the page. But, existing widgets that rely on the inner `.elementor-widget-container` wrapping element to style widgets, can maintain backwards compatibility.

## 小部件标记

旧的、未优化的部件标记包含两个包装元素：

```html
<div class="elementor-widget elementor-widget-{widget-name}">
	<div class="elementor-widget-container">
		...
	</div>
</div>
```

新的、优化的标记只有一个包装元素：

```html
<div class="elementor-widget elementor-widget-{widget-name}">
	...
</div>
```

Elementor 过去曾使用未优化的标记。如今，所有 Elementor 和 Elementor Pro 小部件都使用优化的标记。Elementor 为外部开发者提供了过渡期，以便采用优化的小部件标记。

### 包装元素

每个小部件所需的包装元素数量由小部件开发者决定。Elementor 为外部开发者提供了过渡期，以便采用优化后的小部件标记。

需要两个 `<div>` 包装器（包括内部的 `.elementor-widget-container` 包装器）的旧版小部件，在小部件中使用以下方法：

```php
public function has_widget_inner_wrapper(): bool {
	return true;
}
```

仅需外部 `<div>` 包装器（无需内部的 `.elementor-widget-container` 包装器）即可工作的新版小部件，在小部件中使用以下方法：

```php
public function has_widget_inner_wrapper(): bool {
	return false;
}
```

最后，未使用 `has_widget_inner_wrapper()` 函数的小部件将表现为未优化的、带有两个 `<div>` 包装元素的小部件。此行为在未来可能会改变，以优化剩余的小部件。

### 未来

开发者应提前规划未优化小部件停止渲染的情况。为避免兼容性和样式问题，每个小部件都应包含返回 `false` 的 `has_widget_inner_wrapper()` 方法。

## Examples

### Optimized Widget DOM

To reduce the DOM size, developers can use the `has_widget_inner_wrapper()` method in the widget class, as shown below:

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function has_widget_inner_wrapper(): bool {
		return false;
	}

}
```

This implementation instructs Elementor to render the widget with a single `<div>` wrapper.

### Retaining Unoptimized Widget DOM (for BC)

Legacy widgets that rely on the `.elementor-widget-container` class can continue using the unoptimized DOM by setting the method to return `true`:

```php{4-6,16}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function has_widget_inner_wrapper(): bool {
		return true;
	}

	protected function register_controls(): void {

		$this->add_control(
			'color',
			[
				'label' => esc_html__( 'Color', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::COLOR,
				'selectors' => [
					'{{WRAPPER}} > .elementor-widget-container h3' => 'color: {{VALUE}};',
				],
			]
		);
	}

	protected function render(): void {
		?>
		<h3>
			...
		</h3>
		<?php
	}
}
```

This widget can't use the optimized DOM capability as it uses the inner `.elementor-widget-container` CSS class to style the widget. Therefore, setting `has_widget_inner_wrapper()` to `true` will make sure that Elementor doesn't remove the inner wrapper for this widget.

## 注意事项

请注意，保留未优化的 DOM 结构是一种临时解决方案，旨在让插件开发者在更新代码时保持兼容性。最终目标是将所有小部件过渡到使用优化的单包装器结构。

小部件包装器的 DOM 优化不仅需要将 `has_widget_inner_wrapper()` 设置为 `false`，还需要从所有文件（包括 PHP、CSS 和 JS）中移除 `.elementor-widget-container`。

在上面的示例代码中，只需从选择器中移除 `.elementor-widget-container` 类：

```diff
-	'{{WRAPPER}} > .elementor-widget-container h3' => 'color: {{VALUE}};',
+	'{{WRAPPER}} h3' => 'color: {{VALUE}};',
```
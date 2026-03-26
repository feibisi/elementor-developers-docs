---
title: "Widget Output Caching"
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

## Widget Output Caching

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor offers a feature to minimize the impact of widgets on page performance. For widgets that generate static output, Elementor can cache the HTML, avoiding the need to render it each time the page loads.

By default, Elementor does not cache widget outputs and renders all widgets on the page with every page load. However, developers can enable HTML output caching for widgets to enhance loading speeds.

## 小部件渲染机制

在页面加载期间，Elementor 会渲染所有小部件以生成所需的标记。页面包含的小部件越多，渲染过程就越慢。

为了优化此过程，可以采用 Elementor 的元素缓存机制。"元素缓存"机制会渲染小部件一次，缓存输出结果，并在后续页面加载时使用缓存版本。此操作可将服务器内存使用量减少 99%，并改善前端的[首字节时间](https://web.dev/articles/ttfb)（TTFB）。

### 内容类型

小部件可以返回两种类型的输出：

* **静态内容** - 每次为每个用户返回相同的内容。
* **动态内容** - 返回可能根据不同参数而变化的内容。

静态内容的一个例子是标题小部件，它始终返回来自控件的文本。由于所有用户的输出都相同，因此可以缓存。

相比之下，动态内容涉及根据不同条件改变输出的逻辑。例如，一个包含 PHP 函数来显示用户姓名的小部件，将为不同用户显示不同的结果，因此该小部件不应缓存输出。

动态内容的一个极端例子是每次页面加载时显示随机数的小部件。此类小部件不应缓存其输出。

Elementor 中的小部件缓存机制非常复杂，并包含多个例外情况以避免不适当的缓存。例如，如果小部件的某个控件使用了动态标签或具有显示条件，Elementor 将绕过缓存，完全重新渲染该小部件。

### 缓存输出

为通过缓存静态内容来提升小部件性能，请将以下方法应用于小部件类：

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function is_dynamic_content(): bool {
		return false;
	}

}
```

使用上述代码，小部件会指示 Elementor 在其生成静态内容时缓存其输出。

默认情况下，所有小部件都被视为动态内容且不会被缓存。如果不确定，请避免使用此方法。

### 异常情况

Elementor 的小部件缓存机制非常精密，包含若干例外规则以避免不当缓存。例如，若小部件的某个控件使用了动态标签或设有显示条件，Elementor 将绕过缓存并完整渲染该部件。

## 示例

### 具有静态输出的小部件

假设您有一个包含单个控件的小部件，用户可以在其中设置“标题”。渲染函数将始终为所有用户渲染相同的 HTML，因此输出可以被缓存：

```php {4-6,38-40,51-53}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function is_dynamic_content(): bool {
		return false;
	}

	protected function register_controls(): void {

		$this->start_controls_section(
			'section_content',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'title',
			[
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'placeholder' => esc_html__( 'Enter your title', 'textdomain' ),
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['title'] ) ) {
			return;
		}
		?>
		<h3>
			<?php echo $settings['title']; ?>
		</h3>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.title ) {
			return;
		}
		#>
		<h3>
			{{{ settings.title }}}
		</h3>
		<?php
	}

}
```

### 具有动态输出的小部件

假设您有相同的小部件，但渲染函数包含自定义代码，可能为不同用户生成完全不同的 HTML，因此输出无法被缓存：

```php {34-36,38-40,51-53,55-57}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'section_content',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'title',
			[
				'label' => esc_html__( 'Title', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::TEXT,
				'placeholder' => esc_html__( 'Enter your title', 'textdomain' ),
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['title'] ) ) {
			return;
		}

		if ( is_user_logged_in() ) {
			$greeting = esc_html__( 'Hi logged in user!', 'textdomain' ) . ' ';
		}
		?>
		<h3>
			<?php echo $greeting . $settings['title']; ?>
		</h3>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.title ) {
			return;
		}

		if ( document.body.classList.contains( 'logged-in' ) ) {
			greeting = 'Hi logged in user! ';
		}
		#>
		<h3>
			{{{ greeting + settings.title }}}
		</h3>
		<?php
	}

}
```

这个小部件为登录用户和匿名用户生成不同的 HTML 输出。我们无法缓存小部件的输出，因为缓存的 HTML 可能会显示给错误的用户。

### 测试

测试性能改进时，请确保使用不同类型的小部件——而非同一小部件的多个实例。页面包含的小部件越多、类型越丰富，性能提升效果越显著。接下来，请在 _WordPress 后台 > Elementor > 工具_ 中点击“重新生成文件与数据”按钮。

然后，在您选择的测速工具中，对比首次运行（渲染数据）与第二次运行（缓存数据）的结果。若测量服务器性能，请关注对服务器内存的影响；若测量前端性能，请观察对首字节时间（TTFB）的影响。
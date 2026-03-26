---
title: "控制模板"
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

# 控制模板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

该模板生成在编辑器中显示的最终 HTML。模板使用 JS 通过 `data` JS 对象从设置中返回数据。

## 模板方法

您可以使用相同的 JS 模板来设计用户界面样式。
使用 JS 模板，我们无需通过特殊函数检索数据，Elementor 会为我们处理。来自控件的数据存储在 `data` 变量中：

```php
<?php
class Elementor_Test_Control extends \Elementor\Base_Control {

	public function content_template(): void {
		$control_uid = $this->get_control_uid();
		?>

		<div class="elementor-control-field">

			<# if ( data.label ) {#>
				<label for="<?php echo $control_uid; ?>" class="elementor-control-title">{{{ data.label }}}</label>
			<# } #>

			<div class="elementor-control-input-wrapper elementor-control-unit-5 elementor-control-dynamic-switcher-wrapper">
				<input id="<?php echo $control_uid; ?>" type="{{ data.input_type }}" class="tooltip-target elementor-control-tag-area" data-tooltip="{{ data.title }}" title="{{ data.title }}" data-setting="{{ data.name }}" placeholder="{{ data.placeholder }}" />
			</div>

		</div>

		<# if ( data.description ) { #>
			<div class="elementor-control-field-description">{{{ data.description }}}</div>
		<# } #>

		<?php
	}

}
```
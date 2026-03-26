---
title: "小部件推广"
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

# 小部件推广

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

<img :src="$withBase('/assets/img/elementor-widget-promotion.png')" alt="Elementor Widget Promotion" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

Elementor 小部件在小部件面板中有两个内置位置用于推广和升级销售。

第一个选项是简单的“需要帮助？”链接，这是一个包含小部件通用信息的外部链接。

第二个选项是行动号召区域，提供升级到高级小部件/产品/服务的优惠。

## 小部件帮助链接

帮助链接显示在小部件面板底部所有部分的下方。这是一个内置功能，为用户在所有 Elementor 小部件中提供一致的用户体验。

每个小部件都可以设置一个外部链接，其中包含该特定小部件的通用信息和使用说明。

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	public function get_custom_help_url(): string {
		return 'https://example.com/widget-name';
	}

}
```

## 小部件推广

推广是免费增值插件提供升级销售以升级到高级小部件/产品/服务的一种方式。小部件推广显示在小部件面板的底部。

```php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function get_upsale_data(): array {
		return [
			'condition' => ! \Elementor\Utils::has_pro(),
			'image' => esc_url( ELEMENTOR_ASSETS_URL . 'images/go-pro.svg' ),
			'image_alt' => esc_attr__( 'Upgrade', 'textdomain' ),
			'title' => esc_html__( 'Promotion heading', 'textdomain' ),
			'description' => esc_html__( 'Get the premium version of the widget and grow your website capabilities.', 'textdomain' ),
			'upgrade_url' => esc_url( 'https://example.com/upgrade-to-pro/' ),
			'upgrade_text' => esc_html__( 'Upgrade Now', 'textdomain' ),
		];
	}

}
```

这里需要强调的是，推广是针对特定小部件设置的。它允许插件开发者创建自定义的行动号召来推广该小部件的高级版本。

如果满足某些条件，可以选择性地隐藏/显示此推广。例如，Elementor 仅在 Elementor Pro 未激活时使用小部件推广，因此付费用户不会看到小部件推广。
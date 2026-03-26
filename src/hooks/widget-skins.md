---
title: "小部件皮肤"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Hooks
    - Src
    - Repos
---

# 小部件皮肤

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 提供了一个钩子，允许开发者向小部件应用自定义皮肤。该钩子在小部件构造函数之后运行，并为支持皮肤的特定小部件类型注册自定义皮肤。

## 钩子详情

* **钩子类型:** 动作钩子
* **钩子名称:** `elementor/widget/{$widget_name}/skins_init`
* **说明:** 钩子名称的动态部分 `$widget_name` 指的是小部件名称。
* **影响范围:** 初始化

## 钩子参数

| 参数      | 类型                         | 描述           |
|-----------|------------------------------|----------------|
| `widget`  | _`\Elementor\Widget_Base`_   | 小部件实例     |

#### 示例

让我们为 Google 地图小部件添加一个自定义皮肤：

```php
/**
 * 为 "Google Maps" 小部件添加深色皮肤。
 *
 * @since 1.0.0
 * @param \Elementor\Widget_Base $widget 小部件实例。
 */
function dark_skin_for_google_maps_widget( $widget ) {

	$widget->add_skin( new \MySkins\Skin_Dark_Map( $widget ) );

}
add_action( 'elementor/widget/google_maps/skins_init', 'dark_skin_for_google_maps_widget' );
```
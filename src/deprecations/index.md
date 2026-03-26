---
title: "Elementor 弃用功能"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Deprecations
    - Src
    - Repos
---

# Elementor 弃用功能

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor 是一个不断发展的产品。随着时间的推移，代码会被移除或替换。这些弃用信息会通过各种渠道发布。弃用过程是渐进的，弃用的代码至少经过 8 个主要版本后才会被移除。

## Deprecation Process

The reason for this gradual process is to avoid regression errors caused by external addon developers still using deprecated code. 

Developers are informed of the code change in the [developers blog](https://developers.elementor.com/blog/) and an updated list can be found on the [recent deprecations](https://developers.elementor.com/recent-deprecations/) page.

Elementor's deprecation process consists of the following steps:

<img :src="$withBase('/assets/img/elementor-deprecation-process.png')" alt="Elementor Deprecation Process">

### 软弃用

此阶段持续四个主要 Elementor 版本。在此宽限期内，已弃用的代码不会破坏网站，因为弃用代码和新代码都将按预期工作。但在此阶段使用已弃用代码将显示浏览器控制台通知。

### 硬弃用

此阶段将持续四个额外的 Elementor 主要版本。此宽限期不会破坏网站，因为弃用代码和新代码都将按预期工作。然而，在此阶段使用弃用代码将引发 PHP 错误。

### 删除

经过八个主要版本后，已弃用的代码将从代码库中删除。此时，使用已不存在的代码将引发致命的 PHP 错误，导致网站崩溃。在某些情况下，删除过程可能会推迟到下一个主要版本发布。

## Deprecation Period Example

As an example, if code is deprecated in Elementor 3.1.0, it will start throwing PHP errors in Elementor 3.5.0, and will likely be deleted in Elementor 3.9.0.

<img :src="$withBase('/assets/img/elementor-deprecation-period.png')" alt="Elementor Deprecation Period">

The old deprecated code will be available until its final deletion. The new replacement code will be available from the deprecation point. Between the deprecated and the deletion, the old code and the new code are both available for use.

## 调试已弃用代码

插件开发者应在 `wp-config.php` 文件中将 `WP_DEBUG` 或 `ELEMENTOR_DEBUG` 常量设为 `true` 来测试代码。

启用 WordPress 调试后，软弃用代码会在日志中生成 PHP 通知/警告，硬弃用代码则会在日志中生成 PHP 错误。

## Elementor 如何弃用代码

Elementor 3.1 引入了 `Deprecation` PHP 类来处理上述弃用过程。该类负责处理所有面向开发者的通知，以及（如果需要）所有向后兼容性要求。

Elementor 用于弃用 PHP 代码的主要方法：

* `deprecated_function()` - 处理[函数和方法的弃用过程](src/deprecations/deprecated-function)。
* `deprecated_argument()` - 处理[参数的弃用过程](src/deprecations/deprecated-argument)。
* `do_deprecated_action()` - 处理[动作钩子的弃用过程](src/deprecations/deprecated-action-hook)。
* `apply_deprecated_filter()` - 处理[过滤器钩子的弃用过程](src/deprecations/deprecated-filter-hook)。
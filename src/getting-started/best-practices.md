---
title: "最佳实践"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Getting Started
    - Src
    - Repos
---

# 最佳实践

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

这份最佳实践指南是面向 Elementor 扩展开发者的动态文档，将随着 Elementor 的更新、新功能的引入以及额外建议的提供而不断修订。我们建议遵循这些最佳实践。

## 支持的 PHP 版本

确保您的扩展兼容最常用的 PHP 版本 (v7.4) 以及最新的 PHP 版本 (v8.0 及以上)。

## 兼容性标签

Elementor 拥有自己的 [头部注释](https://developers.elementor.com/docs/addons/plugin-header/)，您可以在其中注明扩展所测试的 Elementor 版本。这是一个可选的头部信息，但我们建议使用它。

## 兼容性检查

[检查网站使用的 Elementor 和 PHP 版本](https://developers.elementor.com/docs/addons/compatibility/)，以确保您的扩展支持该环境。否则，请通知用户网站不满足扩展的要求。

## 脚本与样式注册

Elementor 有其自己的 [注册脚本和样式的方法](https://developers.elementor.com/docs/scripts-styles/)。使用推荐的方法可以确保您的扩展针对性能进行了优化。

## 国际化

使用 WordPress 函数对您的字符串进行 [国际化](https://developer.wordpress.org/apis/internationalization/internationalization-functions/)。

## 移除已弃用的代码

已经拥有一个扩展？请使用 [Elementor 已弃用代码检测器](https://github.com/matipojo/elementor-deprecated-code-detector) 运行检查，查看您的扩展是否包含任何 [已弃用的代码](https://developers.elementor.com/docs/deprecations)。如果是，我们强烈建议将其移除。您可以在此处查看 [近期弃用列表](https://developers.elementor.com/recent-deprecations/)。

## 采用最新的性能特性

实施 [元素缓存](https://developers.elementor.com/elementor-3-22-developers-update/) 以将元素输出存储在缓存中，从而构建性能更高的网站。

## Elementor Pro 开发者许可证

通过申请 [开发者许可证](https://elementor.com/pages/addon-developers-corner/) 来使用 Elementor Pro 进行测试。

## 安全性

参与 Patchstack 免费的 [mVDP 计划](https://elemn.to/patchstack-for-plugins)，通过清晰的漏洞报告结构来维护您产品的安全卫生状况。
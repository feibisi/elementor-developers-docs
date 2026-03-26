---
title: "Composer"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Cli
    - Src
    - Repos
---

# Composer

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

开发者可以通过 [Composer](https://getcomposer.org/) 安装 Elementor 和 Elementor Pro，而无需使用网页浏览器。只需几个简单的 CLI 命令即可完成。

## 什么是 Composer？

Composer 是一个 PHP 依赖管理工具。它简化了在 PHP 项目中安装依赖库的过程。

然而，Composer 本身并不包含 WordPress 插件和主题。为此，开发者使用 [wpackagist.org](https://wpackagist.org/)，这是一个开源服务，它将 WordPress 插件和主题镜像为 Composer 仓库。

## 安装 Elementor

在你的 `composer.json` 文件中注册 WordPress Packagist 仓库：

```json
{
	"repositories": [
		{
			"type": "composer",
			"url": "https://wpackagist.org",
			"only": [
				"wpackagist-plugin/*",
				"wpackagist-theme/*"
			]
		}
	]
}
```

安装最新版本的 Elementor：

```bash
composer require wpackagist-plugin/elementor
```

或者选择特定版本：

```bash
composer require wpackagist-plugin/elementor:3.25.0
```

## 安装 Elementor Pro

在你的 `composer.json` 文件中注册 Elementor 仓库：

```json
{
	"repositories": [
		{
			"type": "composer",
			"url": "https://composer.elementor.com",
			"only": [
				"elementor/elementor-pro"
			]
		}
	]
}
```

配置 composer 以使用 Elementor Pro 许可证密钥：

```bash
composer config --global --auth http-basic.composer.elementor.com token <license-key>
```

要将 Elementor Pro 安装到 `wp-content/plugins` 文件夹而不是 `vendor` 文件夹，请使用 composer 自定义安装器：

```bash
composer config --no-plugins allow-plugins.composer/installers true
composer require composer/installers
```

安装最新版本的 Elementor Pro：

```bash
composer require elementor/elementor-pro
```

或者选择特定版本：

```bash
composer require elementor/elementor-pro:3.25.0
```

## 激活

要激活 Elementor 和 Elementor Pro，请使用以下 WP-CLI 和 [Elementor CLI](src/cli) 命令。

激活 Elementor 插件：

```bash
wp plugin activate elementor
```

激活 Elementor Pro 插件：

```bash
wp plugin activate elementor-pro
```

激活 Elementor Pro 许可证：

```bash
wp elementor-pro license activate <license-key>
```

可选地，你可以在多站点网络中激活 Elementor 和 Elementor Pro：

```bash
wp plugin activate elementor --network
wp plugin activate elementor-pro --network
wp site list --field=url | xargs -n1 -I % wp --url=% elementor-pro license activate <license-key>
```
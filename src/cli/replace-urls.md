---
title: "替换 URL"
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

# 替换 URL

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

更改 URL 的网站，无论是迁移到不同域名还是简单地从 HTTP 转移到 HTTPS，都需要更新数据库中的 URL。Elementor 提供了一个工具，可以在所有 Elementor 页面中将旧 URL 替换为新 URL。Elementor CLI 的 `replace-urls` 命令正是用于此目的。

## 命令

```bash
wp elementor replace-urls <old> <new> [--force]
```

## 参数

`<old>`

_(必需)_ 旧 URL。

`<new>`

_(必需)_ 新 URL。

`[--force]`

_(可选)_ 抑制错误消息。

## 使用示例

```bash
wp elementor replace-urls http://elementor.com https://elementor.com
```

此命令将把所有 `http://elementor.com` HTTP URL 替换为 `https://elementor.com` HTTPS URL。

```bash
wp elementor replace-urls http://elementor.com https://elementor.com --force
```

此命令将把所有 `http://elementor.com` HTTP URL 替换为 `https://elementor.com` HTTPS URL，且不抛出错误。
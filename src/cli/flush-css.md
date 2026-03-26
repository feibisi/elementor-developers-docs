---
title: "刷新 CSS"
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

# 刷新 CSS

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

在 Elementor 中设置的样式保存在数据库中，这些信息用于在 `/wp-content/uploads/elementor/css/` 文件夹中生成 CSS 文件。Elementor CLI 的 `flush-css` 命令将删除所有缓存的 CSS 文件，并使用数据库中存储的最新设置重新创建它们。

## 命令

```bash
wp elementor flush-css [--regenerate] [--network]
```

## 参数

`[--regenerate]`

_(可选)_ 重新创建 CSS 文件。否则，更新的 CSS 文件将在下次访问页面时由 Elementor 创建。

`[--network]`

_(可选)_ 刷新网络中所有站点的 CSS 文件。

## 使用示例

```bash
wp elementor flush-css
```

此命令将刷新所有 Elementor 页面的 CSS 文件。它不会创建新的 CSS 文件，仅刷新旧文件。

```bash
wp elementor flush-css --regenerate
```

此命令将刷新所有 Elementor 页面的 CSS 文件并重新创建新的 CSS 文件。

```bash
wp elementor flush-css --network
```

此命令将刷新网络中所有站点的所有 Elementor 页面的 CSS 文件。
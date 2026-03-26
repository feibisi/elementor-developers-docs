---
title: "清除主题构建器条件"
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

# 清除主题构建器条件

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 主题构建器用于创建网站部件模板。这些模板可以根据预定义的条件进行应用。所有条件都会被缓存。Elementor CLI 的 `theme-builder clear-conditions` 命令将清除缓存的条件，以触发重新生成过程。

## 命令

```bash
wp elementor-pro theme-builder clear-conditions
```

## 参数

无。

## 使用示例

```bash
wp elementor-pro theme-builder clear-conditions
```

此命令将清除条件缓存并重新生成条件。
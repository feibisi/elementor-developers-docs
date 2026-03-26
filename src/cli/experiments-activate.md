---
title: "实验功能激活"
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

# 实验功能激活

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 允许您在实验性功能正式发布前提前使用。您可以通过管理面板或使用 `experiments activate` 命令行来激活实验功能。

## 命令

```bash
wp elementor experiments activate <experiment-name>
```

## 参数

`<experiment-name>`

_(必填)_ 实验功能的名称。

## 使用示例

```bash
wp elementor experiments activate container
```

此命令将激活 `container` 实验功能。
---
title: "实验功能状态"
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

# 实验功能状态

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 的实验功能可以在正式发布前使用。要从命令行检查某个实验功能是处于激活还是未激活状态，请使用 `experiments status` 命令。

## 命令

```bash
wp elementor experiments status <experiment-name>
```

## 参数

`<experiment-name>`

_(必需)_ 实验功能的名称。

## 使用示例

```bash
wp elementor experiments status container
```

此命令将检查 `container` 实验功能是处于 `active`（激活）还是 `inactive`（未激活）状态。
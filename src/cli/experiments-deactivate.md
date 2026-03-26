---
title: "实验功能停用"
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

# 实验功能停用

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 用户可以访问尚未正式发布的实验性功能。这些实验可以从管理面板停用，或通过命令行使用 `experiments deactivate` 命令停用。

## 命令

```bash
wp elementor experiments deactivate <experiment-name>
```

## 参数

`<experiment-name>`

_(必填)_ 实验功能的名称。

## 使用示例

```bash
wp elementor experiments deactivate container
```

此命令将停用 `container` 实验功能。
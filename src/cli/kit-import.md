---
title: "套件导入"
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

# 套件导入

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 套件是模板、页面、弹窗等的集合。您无需单独导入每个模板，可以一次性导入所有内容。套件可以从管理面板导入，也可以使用 `kit import` 命令通过命令行导入。

## 命令

```bash
wp elementor kit import <file-path> [--include] [--overrideConditions] [--sourceType]
```

## 参数

`<file-path>`

_(必需)_ 套件文件的路径。

`[--include]`

_(可选)_ 导入时要包含的数据类型。可能的值有 `content`、`templates`、`site-settings`。如果未指定此参数，则将包含所有数据类型。

`[--overrideConditions]`

_(可选)_ 需要覆盖条件的模板 ID。

`[--sourceType]`

_(可选)_ 当前会话中使用的源类型。可用值为 `local`、`remote`、`library`。默认值为 `local`。

## 使用示例

```bash
wp elementor kit import path/to/elementor-kit.zip
```

此命令将导入整个套件文件的内容。

```bash
wp elementor kit import path/to/elementor-kit.zip --include=site-settings,content
```

此命令将仅导入站点设置和内容。

```bash
wp elementor kit import path/to/elementor-kit.zip --overrideConditions=3478,4520
```

此命令将导入所有内容，并为给定的模板 ID 覆盖条件。

```bash
wp elementor kit import path/to/elementor-kit.zip --unfilteredFilesUpload=enable
```

此命令将允许导入过程导入未经过滤的文件。
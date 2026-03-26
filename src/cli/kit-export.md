---
title: "套件导出"
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

# 套件导出

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

导出多个独立模板并非易事。Elementor 可以将网站的所有内容、模板和站点设置打包成一个套件进行导出。这些套件可以从管理面板导出，也可以通过命令行使用 `kit export` 命令导出。

## 命令

```bash
wp elementor kit export <file-path> [--include]
```

## 参数

`<file-path>`

_(必需)_ 套件文件的路径。

`[--include]`

_(可选)_ 要包含在导出中的数据类型。可能的值包括 `content`、`templates`、`site-settings`。如果未指定此参数，则将包含所有数据类型。

## 使用示例

```bash
wp elementor kit export path/to/export-file-name.zip
```

此命令会将所有站点数据导出到指定的文件名。

```bash
wp elementor kit export path/to/export-file-name.zip --include=site-settings,content
```

此命令将仅导出站点设置和内容到指定的文件名。
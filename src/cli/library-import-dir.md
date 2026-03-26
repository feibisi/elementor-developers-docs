---
title: "库导入目录"
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

# 库导入目录

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

逐个导入模板非常耗时。您可以一次性导入目录中的所有模板。Elementor CLI 的 `library import-dir` 命令将通过命令行导入所有模板 JSON 文件。

## 命令

```bash
wp elementor library import-dir <dir-path>
```

## 参数

`<dir-path>`

_(必需)_ 目录的路径。

## 使用示例

```bash
wp elementor library import-dir path/to/custom-templates/
```

此命令将把 `path/to/custom-templates/` 目录中的所有模板 JSON 文件导入到库中。
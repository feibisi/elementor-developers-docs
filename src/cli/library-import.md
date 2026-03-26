---
title: "库导入"
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

# 库导入

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

用户可以通过上传单个模板 JSON 文件或包含多个 JSON 文件的 ZIP 文件，从库中导入 Elementor 模板。Elementor CLI 的 `library import` 命令将通过命令行导入模板。

## 命令

```bash
wp elementor library import <file-path> [--returnType]
```

## 参数

`<file-path>`

_(必需)_ 模板文件的路径。

`[--returnType]`

_(可选)_ 输出格式。可用值为 `ids` 和 `info`。默认为 `info`。

## 使用示例

```bash
wp elementor library import path/to/elementor-12345-2022-03-04.json
```

此命令将把 `path/to/elementor-12345-2022-03-04.json` 模板导入到库中。

```bash
wp elementor library import path/to/elementor-12345-2022-03-04.json --returnType=ids
```

此命令将把 `path/to/elementor-12345-2022-03-04.json` 模板导入到库中，并返回已导入项目的 ID。
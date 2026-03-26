---
title: "库同步"
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

# 库同步

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor 在本地维护着一个可从 Elementor 模板库下载的可用模板列表。系统会安排一个临时任务，每 12 小时同步一次可用模板。Elementor CLI 的 `library sync` 命令可通过命令行触发从云端进行的同步。

## 命令

```bash
wp elementor library sync [--force] [--network]
```

## 参数

`[--force]`

_(可选)_ 即使库看起来已经是最新状态，也强制进行库同步。

`[--network]`

_(可选)_ 为网络中的每个站点同步库。

## 使用示例

```bash
wp elementor library sync
```

此命令将使用 Elementor 云端库同步本地库。

```bash
wp elementor library sync --force
```

即使库看起来已经是最新状态，此命令也将使用 Elementor 云端库进行同步。

```bash
wp elementor library sync --network
```

此命令将为网络中的每个站点使用 Elementor 云端库同步其库。
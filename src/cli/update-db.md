---
title: "更新数据库"
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

# 更新数据库

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

在某些情况下，新的 Elementor 版本会对数据库执行更改（例如迁移到套件、用全局样式替换方案等）。Elementor CLI 的 `update db` 命令将通过命令行触发数据库更新功能。

## 命令

```bash
wp elementor update db [--force] [--network]
```

和

```bash
wp elementor-pro update db [--force] [--network]
```

## 参数

`[--force]`

_(可选)_ 即使看起来更新正在进行中，也强制更新数据库。

`[--network]`

_(可选)_ 为网络中的每个站点更新数据库。

## 使用示例

```bash
wp elementor update db
```

此命令将在需要时更新数据库。

```bash
wp elementor-pro update db
```

此命令将在需要时更新 Elementor Pro 数据库。

```bash
wp elementor update db --force
```

此命令将在另一个进程正在运行时也更新数据库。

```bash
wp elementor update db --network
```

此命令将为网络中的每个站点更新数据库。
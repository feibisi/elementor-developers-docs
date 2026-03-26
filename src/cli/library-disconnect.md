---
title: "库断开连接"
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

# 库断开连接

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

通过命令行断开站点与 Elementor 库的连接，只需提供 WordPress 用户信息。

## 命令

```bash
wp elementor library disconnect [--user]
```

## 参数

`[--user]`

_(可选)_ 要断开的用户。接受用户 ID、用户登录名或电子邮件。

## 使用示例

```bash
wp elementor library disconnect --user=admin
```

此命令将断开 WordPress `admin` 用户与 Elementor 库的连接。
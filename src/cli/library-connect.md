---
title: "Library Connect"
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

# Library Connect

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

通过命令行将站点连接到 Elementor 库，只需提供 WordPress 用户和连接令牌。

## 命令

```bash
wp elementor library connect [--user] [--token]
```

## 参数

`[--user]`

_(可选)_ 要连接的用户。接受用户 ID、用户登录名或电子邮件。

`[--token]`

_(可选)_ 来自 Elementor 账户仪表板的连接令牌。

## 使用示例

```bash
wp elementor library connect --user=admin --token=xxx
```

此命令将把 WordPress `admin` 用户连接到 Elementor 库。

## 注意事项

::: warning 注意
此命令由 Elementor 团队使用，用于与 Elementor 服务器连接，以便通过 CLI 更新库以进行测试和调试。目前，外部开发者无法获取 `token`。
:::
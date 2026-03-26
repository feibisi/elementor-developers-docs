---
title: "系统信息"
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

# 系统信息

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

系统信息显示网站配置的详细信息。这些数据可用于调试问题，帮助开发人员和支持工程师识别问题。Elementor CLI 的 `system info` 命令将以 JSON 格式打印站点的系统信息。

## 命令

```bash
wp elementor system-info
```

## 参数

无。

## 使用示例

```bash
wp elementor system-info
```

此命令将显示完整的系统信息。
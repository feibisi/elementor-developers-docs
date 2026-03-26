---
title: "Elementor 表单操作"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Form Actions
    - Src
    - Repos
---

# Elementor 表单操作

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

表单操作是访客提交数据后执行的任务。一个操作可以通过电子邮件发送表单数据、将其重定向到其他页面，或将数据发送到外部营销服务——可能性是无限的。

Elementor Pro 提供了一套工具来添加您自己的自定义操作。

<img :src="$withBase('/assets/img/elementor-form-actions.png')" alt="Elementor Form Actions" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

## 操作

当用户向页面添加表单小部件时，他们可以选择访客提交表单后将执行的操作。选择一个操作会将其设置添加到一个独立的部分中。

## 可用操作

表单小部件默认包含以下操作：

*   **收集提交**
*   **电子邮件**
*   **电子邮件 2**
*   **重定向**
*   **Webhook**
*   **MailChimp**
*   **Drip**
*   **ActiveCampaign**
*   **GetResponse**
*   **ConvertKit**
*   **MailerLite**
*   **Slack**
*   **Discord**
*   **弹出窗口**

## 管理表单操作

外部开发者可以注册新的表单操作。了解更多：

*   [添加新操作](src/form-actions/add-new-action)

## 创建表单操作

了解更多关于操作的结构以及如何创建您自己的操作：

*   [操作结构](src/form-actions/action-structure)
*   [操作数据](src/form-actions/action-data)
*   [操作控件](src/form-actions/action-controls)
*   [操作运行](src/form-actions/action-run)
*   [导出时的操作](src/form-actions/action-on-export)

## 代码示例

看看添加新操作是多么容易：

*   [简单示例](src/form-actions/simple-example)
*   [高级示例](src/form-actions/advanced-example)
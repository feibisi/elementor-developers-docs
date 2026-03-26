---
title: "Elementor 表单字段"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Form Fields
    - Src
    - Repos
---

# Elementor 表单字段

<Badge type="tip" vertical="top" text="Elementor Pro" /> <Badge type="warning" vertical="top" text="Advanced" />

**Elementor 表单小部件** 是一个高级但易于使用的工具，用于创建网页表单。该小部件使得使用数十种字段类型来创建和设计任何表单变得轻而易举。

<img :src="$withBase('/assets/img/elementor-form-fields.png')" alt="Elementor Form Fields" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

## 表单字段

当用户将表单小部件添加到页面时，他们可以选择在表单中显示哪些字段。

Elementor 使用 "Repeater" 控件允许用户向表单添加多个字段。对于每个字段，用户可以从可用字段列表中选择字段类型。

## 可用字段

表单小部件开箱即用，包含以下字段：

* **文本** (`text`)
* **电子邮件** (`email`)
* **文本域** (`textarea`)
* **URL** (`url`)
* **电话** (`tel`)
* **单选按钮** (`radio`)
* **选择框** (`select`)
* **复选框** (`checkbox`)
* **同意条款** (`acceptance`)
* **数字** (`number`)
* **日期** (`date`)
* **时间** (`time`)
* **文件上传** (`upload`)
* **密码** (`password`)
* **HTML** (`html`)
* **隐藏字段** (`hidden`)
* **步骤** (`step`)
* **reCAPTCHA** (`recaptcha`)
* **reCAPTCHA V3** (`recaptcha_v3`)
* **蜜罐** (`honeypot`)

## 管理表单字段

外部开发者可以注册新字段或注销现有字段。了解更多操作方法：

* [移除字段](src/form-fields/remove-fields)
* [添加新字段](src/form-fields/add-new-field)

## 创建表单字段

外部开发者可以了解更多关于字段结构以及如何创建自己的字段：

* [字段结构](src/form-fields/field-structure)
* [字段数据](src/form-fields/field-data)
* [字段渲染](src/form-fields/field-render)
* [字段验证](src/form-fields/field-validation)
* [字段控件](src/form-fields/field-controls)
* [字段内容模板](src/form-fields/field-content-template)
* [字段依赖关系](src/form-fields/field-dependencies)

## 代码示例

看看添加新字段是多么容易：

* [简单示例](src/form-fields/simple-example)
* [高级示例](src/form-fields/advanced-example)
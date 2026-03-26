---
title: "历史面板"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor
    - Src
    - Repos
---

# 历史面板

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/history-panel.png')" alt="Elementor History Panel" style="float: right; width: 300px; margin-left: 20px; margin-bottom: 20px;">

**历史**是[编辑器](src/editor)中的一个面板，允许用户查看其最新操作和修订版本。此面板让用户可以撤销/重做操作，并恢复页面的先前版本。

## 结构与功能

该面板包含两个选项卡：

* **修订版本** - 保存在数据库中的页面版本。
* **操作** - 自上次保存页面以来所做的页面更改。

修订版本是 WordPress 的功能，Elementor 只是让恢复 WordPress 数据库中已保存的不同修订版本变得更加容易。

另一方面，操作是用户在 Elementor 内部所做的更改。该面板可以轻松显示更改并撤销/重做这些更改。
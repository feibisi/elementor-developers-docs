---
title: "右键菜单操作"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Context Menu
    - Src
    - Repos
---

# 右键菜单操作

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

右键菜单弹窗包含多个组，这些组内包含称为“操作”的项。操作应用于选定的元素（区块、列、小部件）。在底层，这些操作是 JS 回调函数。

## 操作对象

操作是一个包含以下属性和方法的 JS 对象：

```js
const action = {
	name: 'action-id',
	icon: 'eicon-code',
	title: 'Action Label',
	shortcut: '',
	isEnabled: () => true,
	callback: () => {},
};
```

*   **操作名称** - 代码中使用的唯一 ID。
*   **操作图标** - 操作图标，可在 [Elementor Icons](https://elementor.github.io/elementor-icons/) 或 [FontAwesome Icons](https://fontawesome.com/) 中找到。
*   **操作标题** - 向用户显示的标签。
*   **操作快捷键** - 触发操作的键盘快捷键。
*   **是否启用** - 定义操作是启用还是禁用。
*   **操作回调** - 应用于选定元素的 JS 回调函数。

::: warning 请注意
操作键盘快捷键将不在文档中介绍，因为它需要额外的 JS 组件配置。
:::

## 管理操作

通过挂钩到 JS `elements/context-menu/groups` 过滤器钩子，您可以添加、修改或删除操作项。

*   [添加新操作](src/context-menu/add-new-action)
*   [移除操作](src/context-menu/remove-action)
*   [更新操作](src/context-menu/update-action)
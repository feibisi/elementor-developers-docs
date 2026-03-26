---
title: "API - `$e.hooks`"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Js
    - Src
    - Repos
---

# API - `$e.hooks`

`$e.hooks` API 是 `$e.hooks.ui` 和 `$e.hooks.data` 的管理器。它允许你创建自定义钩子。这些钩子附加到 `$e.commands`，每个钩子在通过 `$e.run()` 运行命令的 _之前/之后_ 触发。

**位置**: `core/common/assets/js/api/core/hooks.js`

## 方法

| Method                              | Params                                                                                         |  Returns              | Description                                                         |
|-------------------------------------|------------------------------------------------------------------------------------------------|-----------------------|---------------------------------------------------------------------|
| `$e.hooks.activate()`               |                                                                                                |                       | Activate all hooks.                                                 |
| `$e.hooks.deactivate()`             |                                                                                                |                       | Deactivate all hooks.                                               |
| `$e.hooks.getAll()`                 |                                                                                                | `{Array}`             | Receive all loaded hooks.                                           |
| `$e.hooks.register()`               | `{String}` *type*, `{String}` *event*, `{HookBase}` *instance*                                 | `{Object}` *callback* | Register a hook.                                                    |
| `$e.hooks.run()`                    | `{String}` *type*, `{String}` *event*, `{String}` *command*, `{Object}` *args*, `{*}` *result* | `{Boolean}`           | Run a hook.                                                         |
| `$e.hooks.registerDataAfter()`      | `{HookBase}` *instance*                                                                        | `{Object}` *callback* | Register data hook that runs after the command runs.                |
| `$e.hooks.registerDataCatch()`      | `{HookBase}` *instance*                                                                        | `{Object}` *callback* | Register data hook that runs when the command fails.                |
| `$e.hooks.registerDataDependency()` | `{HookBase}` *instance*                                                                        | `{Object}` *callback* | Register data hook that runs before the command runs as dependency. |
| `$e.hooks.registerUIAfter()`        | `{HookBase}` *instance*                                                                        | `{Object}` *callback* | Register UI hook that runs after the commands run.                  |
| `$e.hooks.registerUICatch()`        | `{HookBase}` *instance*                                                                        | `{Object}` *callback* | Register UI hook that runs when the command fails.                  |
| `$e.hooks.registerUIBefore()`       | `{HookBase}` *instance*                                                                        | `{Object}` *callback* | Register UI hook that runs before the command.                      |
| `$e.hooks.runDataAfter()`           | `{String}` *command*, `{Object}` *args*, `{*}` *result*                                        | `{Boolean}`           | Run a data hook that runs after the command.                        |
| `$e.hooks.runDataCatch()`           | `{String}` *command*, `{Object}` *args*, `{*}` *result*                                        | `{Boolean}`           | Run a data hook that runs when the command fails.                   |
| `$e.hooks.runDataDependency()`      | `{String}` *command*, `{Object}` *args*, `{*}` *result*                                        | `{Boolean}`           | Run a data hook that runs before the command as dependency.         |
| `$e.hooks.runUIAfter()`             | `{String}` *command*, `{Object}` *args*, `{*}` *result*                                        | `{Boolean}`           | Run a UI hook that runs after the commands run.                     |
| `$e.hooks.runUICatch()`             | `{String}` *command*, `{Object}` *args*, `{*}` *result*                                        | `{Boolean}`           | Run a UI hook that runs when the command fails.                     |
| `$e.hooks.runUIBefore()`            | `{String}` *command*, `{Object}` *args*, `{*}` *result*                                        | `{Boolean}`           | Run a UI hook that runs before the command.                         |

## 指南

* 每个钩子都由一个[组件](src/js/components)拥有。

* 每个[组件](src/js/components)都可以扩展 `defaultHooks` 方法，该方法用于导入钩子。

* 钩子通过内置方法 `importHooks` 导入。
  * 所有钩子应在一个索引文件中导出：

```javascript
// index.js
export { FooterSaverRefreshMenu } from './ui/document/elements/settings/footer-saver-refresh-menu';
export { UpdateButton } from './ui/document/save/set-is-modifed/update-button';
export { BypassImport } from './data/document/elements/import/bypass-import';
export { SaveExtras } from './data/document/save/save/save-extras';
```

你可以在 `component/hooks/what-ever-you-wish` 下的每个层级中拥有任意多个索引文件来组织代码，但要求必须在 `component/hooks/index.js` 处有一个索引文件来导出所有钩子。以上面的 **index.js** 为例：

```
📦 component
│   📜 component.js
│
└───📂 hooks
│   │   📜 index.js ( 导出所有钩子 )
│   │
│   └───📂 ui
│   │   └───📂 document
│   │   │   └───📂 elements
│   │   │   │   └───📂 settings
│   │   │   │   │   │   📜 footer-saver-refresh-menu.js
│   │   │   │   │   │   ...
│   │   │   └───📂 save
│   │   │   │   └───📂 set-is-modfifed
│   │   │   │   │   │   📜 update-button.js
│   │   │   │   │   │   ...
│   │   📜 index.js ( 导出所有 ui 钩子 )
│   │   ...
│   └──📂 data
│   │   └───📂 document
│   │   │   └───📂 elements
│   │   │   │   └───📂 import
│   │   │   │   │   │   📜 bypass-import.js
│   │   │   │   │   │   ...
│   │   │   └───📂 save
│   │   │   │   └───📂 save
│   │   │   │   │   │   📜 save-extras.js
│   │   │   │   │   │   ...
│   │   📜 index.js ( 导出所有 data 钩子 )
│   │   ...
```

`component/hooks/index.js` 文件第 _5_ 行：

```javascript
export * from './ui/';
export * from './data/';
```

`component/hooks/ui/index.js` 文件第 _17_ 行：

```javascript
export { FooterSeverRefreshMenu } from './document/elements/settings/footer-saver-refresh-menu';
export { UpdateButton } from './document/save/set-is-modifed/update-button';
```

`component/hooks/data/index.js` 文件第 _29_ 行：

```javascript
export { BypassImport } from './document/elements/import/bypass-import';
export { SaveExtras } from './document/save/save/save-extras';
```

使用 `importHooks` 示例：`component/component.js` 文件第 _2_ 行：

```javascript
import * as hooks from './hooks/';

export class Component extends $e.modules.ComponentBase {
    getNamespace() {
        return 'component-name';
    }

    defaultHooks() {
        return this.importHooks( hooks );
    }
}
```

## Conventions

```javascript
// {FILE_PATH}/{FILE_NAME} - This is line should be deleted - just for the example.
import HookUIAfter from 'elementor-api/modules/hooks/{TYPE}/after';

export class {FILE_NAME_CAMEL_CASE} extends HookUIAfter {
	getCommand() {
		return '{COMMAND}';
	}

	getId() {
		return '{FILE_NAME_WITHOUT_JS}--{COMMAND}';
	}

	getContainerType() {
		return '{CONTAINER_TYPE}';
	}

	getConditions( args ) {
		return args.settings && 'undefined' !== typeof args.settings.post_status;
	}

	apply( args ) {
		const { footerSaver } = $e.components.get( 'document/save' );

		footerSaver.setMenuItems( args.container.document );

		footerSaver.refreshWpPreview();
	}
}

export default {FILE_NAME_CAMEL_CASE};
```

### Legend

| Name                   | Format  - Description               | Value for example. 
|------------------------|-------------------------------------|---------------------
|`{TYPE}`                | `ui` or `data` depends on the hook  | `ui`
|`{COMMAND}`             | which command to hook               | `document/elements/settings`
|`{FILE_NAME}`           | kebab case, name is description oh what the hook does | `footer-saver-refresh-menu.js`
|`{FILE_NAME_CAMEL_CASE}`| camel case, of `{FILE_NAME}`        | `FooterSaverRefreshMenu`
|`{FILE_NAME_WITHOUT_JS}`| `{FILE_NAME}` without `.js`         | `footer-saver-refresh-menu`
|`{FILE_PATH}`           | `{TYPE}/{COMMAND}/{FILE_NAME}`      | `ui/document/elements/settings/footer-saver-refresh-menu.js`
|`{CONTAINER_TYPE}`      | optional, gain performance if container type is known in advance | `document`

### 示例

```javascript
// ui/document/elements/settings/footer-saver-refresh-menu.js - 此行应删除 - 仅用于示例。
import HookUIAfter from 'elementor-api/modules/hooks/ui/after';

export class FooterSaverRefreshMenu extends HookUIAfter {
	getCommand() {
		return 'document/elements/settings';
	}

	getId() {
		return 'footer-save-refresh-menu--document/elements/settings';
	}

	getContainerType() {
		return 'document';
	}

	getConditions( args ) {
		return args.settings && 'undefined' !== typeof args.settings.post_status;
	}

	apply( args ) {
		const { footerSaver } = $e.components.get( 'document/save' );

		footerSaver.setMenuItems( args.container.document );

		footerSaver.refreshWpPreview();
	}
}

export default FooterSaverRefreshMenu; // 必需 - 注释应删除。
```

::: warning 注意
关于如何使用钩子的更多信息，可根据其类型在 [`{$e.hooks.ui}`](src/js/hooks/ui) 和 [`{$e.hooks.data}`](src/js/hooks/data) 中找到。
:::
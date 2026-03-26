---
title: "API -- `$e.commands`"
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

# API -- `$e.commands`

新的 Commands API（自 2.7.0 版本起）提供了一种简单便捷的方式，通过 JS 命令在编辑器中运行某些操作、创建小部件，以及显示通知或撤销更改。

可通过以下方式获取完整命令列表（包括自定义和第三方命令）：`$e.commands.getAll();`

* **描述**：`$e.commands` API 是所有 _命令_ 的管理器，允许您创建通过 `$e.run()` 运行的自定义 _命令_。每个组件都有其独特的命令，所有命令都由该 **API** 管理。

* **位置**：`/core/common/assets/js/components/commands.js`

* **父级**：`elementorModules.Module`

* **可用命令**：有关 **所有** 命令的更多信息，请访问 [`{$e.commands.getAll()}`](src/js/commands-methods/getall) **方法**。

## 方法

| Method                               | Params                                                                                 | Returns                         | Description                                                                         |
|--------------------------------------|----------------------------------------------------------------------------------------|---------------------------------|-------------------------------------------------------------------------------------|
| `$e.commands.getAll()`               |                                                                                        |                                 | Receive all loaded commands.                                                        |
| `$e.commands.register()`             | `{(BaseComponent⎮string)}` *component*, `{String}` command, `{function()}` *callback* | `{Commands}` *$e.commands*      | Register new command.                                                               |
| `$e.commands.getComponent()`         | `{String}` *command*                                                                   | `{BaseComponent)`               | Receive Component of the command.                                                   |
| `$e.commands.is()`                   | `{String}` *command*                                                                   | `{Boolean}`                     | Checks if current running command is the same parameter command.                    |
| `$e.commands.isCurrentFirstTrace()`  | `{String}` *command*                                                                   | `{Boolean}`                     | Checks if parameter command is the first command in trace that currently running.   |
| `$e.commands.getCurrent()`           |                                                                                        | `{Object}`                      | Receive currently running components and its commands.                              |
| `$e.commands.getCurrentArgs()`       |                                                                                        | `{Object}`                      | Receive currently running command args.                                             |
| `$e.commands.getCurrentFirst()`      |                                                                                        | `{String}`                      | Receive first command that currently running.                                       |
| `$e.commands.getCurrentFirstTrace()` |                                                                                        | `{Object}`                      | Receive first command in trace that currently running.                              |
| `$e.commands.beforeRun()`            | `{String}` *command*, `{Object}` *args*                                                | `{Boolean}` *dependency result* | Method fired before the command runs.                                               |
| `$e.commands.run()`                  | `{String}` *command*, `{Object}` *args*                                                | `{}` *results*                  | Runs a command.                                                                     |
| `$e.commands.runShortcut()`          | `{String}` *command*, *event*                                                          | `{}` *results*                  | Run shortcut.                                                                       |
| `$e.commands.afterRun()`             |                                                                                        |                                 | Method fired after the command runs.                                                |
| `$e.commands.error()`                | `{String}` *message*                                                                   |                                 | Throws error.                                                                       |

## Examples

```javascript
// Example create and register new command.
// Important: Available to run in the console does not depends on anything else.

class ExampleCommand extends $e.modules.CommandBase {
	apply( args ) {
		// Output command args to console.
		console.log( 'ExampleCommand: ', args );

		// Return object as example.
		return {
			example: 'result from ExampleCommand',
		};
	}
}

class CustomComponent extends $e.modules.ComponentBase {
	getNamespace() {
		return 'custom-component';
	}

	defaultCommands() {
		// Object of all the component commands.
		return {
			example: ( args ) => ( new ExampleCommand( args ) ).run(),
		};
	}
}

// Register the new component.
$e.components.register( new CustomComponent() );

// Run's 'example' command from 'custom-component'.
result = $e.run( 'custom-component/example', {
	property: 'value',
} );

// Output command run result.
console.log( 'e-commands-eg-1-result: ', result );
```

## 指南

* 每个命令都应归属于某个[组件](src/js/components)。
* 目前，主要有 *3* 种*基础类型*：
  * 命令 - 基类：`$e.modules.CommandBase` - `[用户]` 命令，代表用户操作。
  * 内部命令 - 基类：`$e.modules.CommandInternalBase` - `[内部]` 供内部使用。
  * 数据命令 - 基类：`$e.modules.CommandData` - `[数据]` 命令，用于与*数据\缓存\后端*通信。
* 每个[组件](src/js/components)可以重写几个方法：`defaultCommands`、`defaultCommandsInternal`、`defaultData`，这些方法用于根据命令类型导入命令。
* 命令应通过内置方法 `importCommands` 导入。
  * 示例：

```
📦 组件
│   📜 component.js
│
└───📂 commands
│   │   📜 index.js ( 导出所有命令 )
│   │   📜 example-command.js
│   │   ...
```

`component/commands/index.js` 文件第 _5_ 行：

```javascript
export { ExampleCommand } from './example-command';
```

使用 `importCommands` 示例：`component/component.js` 文件第 _2_ 行：

```javascript
import * as commands from './commands/';

export class Component extends $e.modules.ComponentBase {
    getNamespace() {
        return 'component-name';
    }

    defaultCommands() {
        return this.importCommands( commands );
    }
}
```

* 所有系列的命令类型都应具有唯一的文件夹和索引文件来存放它们：
  * 命令：
    * 如上例所示。
  * 内部命令
    * 示例：

```
📦 组件
│   📜 component.js
│
└───📂 commands-internal
│   │   📜 index.js ( 导出所有命令 )
│   │   📜 internal-command.js
│   │   ...
```

`component/commands-internal/index.js` 文件第 _5_ 行：

```javascript
export { InternalCommand } from './internal-command';
```

使用 `importCommands` 示例：`component/component.js` 文件第 _2_ 行：

```javascript
import * as commandsInternal from './commands-internal/';

export class Component extends $e.modules.ComponentBase {
	getNamespace() {
		return 'component-name';
	}

	defaultCommandsInternal() {
		return this.importCommands( commandsInternal );
	}
}
```

* 数据命令

```
📦 组件
│   📜 component.js
│
└───📂 commands-data
│   │   📜 index.js ( 导出所有命令 )
│   │   📜 data-command.js
│   │   ...
```

`component/commands-data/index.js` 文件第 _5_ 行：

```javascript
export { DataCommand } from './data-command';
```

使用 `importCommands` 示例：`component/component.js` 文件第 _2_ 行：

```javascript
import * as commandsData from './commands-data/';

export class Component extends $e.modules.ComponentBase {
	getNamespace() {
		return 'component-name';
	}

	defaultData() {
		return this.importCommands( commandsData );
	}
}
```

::: warning 注意
关于 [`{$e.modules.CommandBase}`](src/modules/command-base.full) 类的更多信息。
:::
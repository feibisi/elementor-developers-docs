---
title: "控件类型"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor Controls
    - Src
    - Repos
---

# 控件类型

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

Elementor 开箱即用，包含了种类繁多的控件。每个控件都有一个自定义模板以及可选的默认设置、默认值和其他影响控件在面板中输出的方法。

## 基础控件

Elementor 有几个扩展自抽象基类的基础控件，每个都用于不同的目的：

*   **数据控件** – 返回单个值的控件。
*   **多值控件** – 返回多个值的控件。
*   **单位控件** – 返回基于单位的值的控件。
*   **UI 控件** – 仅在面板中可见且不返回值的 UI 元素。
*   **组控件** – 将多个控件组合在一起。

## 继承关系

在底层，上述抽象基类是通过扩展 `\Elementor\Base_Control` 抽象类创建的，并继承了其属性和方法。您在编辑器中看到的所有其他控件都扩展自这些基础控件。

```
Base_Control
|
├─ Base_Data_Control
|  ├─ ...
|  └─ ...
|
├─ Control_Base_Multiple
|  ├─ ...
|  └─ ...
|
├─ Control_Base_Units
|  ├─ ...
|  └─ ...
|
├─ Base_UI_Control
|  ├─ ...
|  └─ ...
|
└─ Group_Control_Base
   ├─ ...
   └─ ...
```

## 扩展控件

### 扩展数据控件

要创建您自己的数据控件，您需要扩展 `\Elementor\Base_Data_Control` 抽象类：

```php {1}
class Elementor_Test_Control extends \Elementor\Base_Data_Control {
}
```

### 扩展多值控件

要创建您自己的多值控件，您需要扩展 `\Elementor\Control_Base_Multiple` 抽象类：

```php {1}
class Elementor_Test_Control extends \Elementor\Control_Base_Multiple {
}
```

### 扩展单位控件

要创建您自己的单位控件，您需要扩展 `\Elementor\Control_Base_Units` 抽象类：

```php {1}
class Elementor_Test_Control extends \Elementor\Control_Base_Units {
}
```

### 扩展 UI 控件

要创建您自己的 UI 控件，您需要扩展 `\Elementor\Base_UI_Control` 抽象类：

```php {1}
class Elementor_Test_Control extends \Elementor\Base_UI_Control {
}
```

### 扩展组控件

要创建您自己的组控件，您需要扩展 `\Elementor\Group_Control_Base` 抽象类：

```php {1}
class Elementor_Test_Control extends \Elementor\Group_Control_Base {
}
```
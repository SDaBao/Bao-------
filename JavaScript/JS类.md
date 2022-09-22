# 类

## 基本语法

```JS
class MyClass {
  // class 方法
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```

- `new` 会自动调用构造函数的方法，在 `constructor()` 中初始化对象
- `class` 是一个函数，这个函数是 `constructor` 方法
- `class` 不仅是一个语法糖，函数定义与类定义的结果有巨大差异
  - `class` 创建的函数具有特殊的内部属性标记 `[[IsClassConstructor]]: true`，必须使用 `new` 调用
  - 类的方法不可枚举，原型中所有方法的 `enumerable` 标志为 false
  - 类总是使用 `use strict` 严格模式

- 类可以通过表达式创建，类似于命名函数表达式 NFE
- 类可能包括 getters/setters 、计算属性等
  - 计算属性用中括号表示名称 `['say' + 'Hi']() { alert("Hello"); }` （类似于对象字面量）
- `class` 字段允许添加任何属性的语法

## 类继承 extends

拓展类的一种方式，`extends` 后可以指定任意表达式

`class Rabbit extends Animal` 将 `Rabbit.prototype.[[Prototype]]` 设置为 `Animal.prototype`

### 重写方法 super

- 执行 `super.method(...)` 来调用一个父类方法。
- 执行 `super(...)` 来调用一个父类 `constructor`（只能在我们的 `constructor` 中）。

> 箭头函数没有 `super`，会从外部获取

### 重写 constructor

- 类扩展未定义 `constructor` 会自动生成
- 自定义的 `constructor` 必须调用 `super(...)`，并且必须在 `this` 前调用
- 父构造器总会调用自己字段的值，而不是在子类中被重写的值
  - 类字段：基类在构造函数调用前初始化，派生类在 `super()` 后初始化。因此在子类调用父类构造函数时子类的字段值还未初始化（重写的方法不会出现这种情况）

- `[[HomeObject]]` 函数内部属性，记住了它们的类/对象——super由此解析父方法。（带有`super`的方法复制到另一个对象是不安全的）

## 静态属性和静态方法

`static` 关键字标记 

静态方法：用于整个类的方法，不适用于单个对象（与类的实例无关）
静态属性：用于存储类级别的数据，静态声明与直接给类本身赋值相同（新增加的特性）

继承关系：静态属性和方法均可被继承，子类的 `[[prototype]]` 指向父类

## 私有的和受保护的属性和方法

OOP的一个重要原则——将内部和外部接口分隔开（其划分被称为封装）

- 内部接口 —— 可以通过该类的其他方法访问，但不能从外部访问的方法和属性。
- 外部接口 —— 也可以从类的外部访问的方法和属性。

- 公共的：可从任何地方访问。它们构成了外部接口。
- 私有的：只能从类的内部访问。这些用于内部接口。
- “受保护”的字段：只能从类的内部和基于其扩展的类的内部访问（可被继承）

- 私有属性使用 `#` 表示（新规范，支持不完全）

可支持性：严格界定内部接口，可以自由修改内部属性和方法，而不用通知使用者

隐藏复杂性：实施细节被隐藏，并提供简单的有据可查的外部接口（使用受保护或私有的属性）。

## 扩展内建类

扩展方法：

```JS
class PowerArray extends Array {
  isEmpty() {
    return this.length === 0;
  }
}
```

> 使用内建方法会返回子类的对象，使用 `Symbol.species` 返回 Array，使 map 或 filter 这样的内建方法返回常规数组。

- 内建类有自己的静态方法，但不会继承静态方法

## `instanceof` 类检查

`instanceof` 操作符用于检查一个对象是否属于某个特定的 class（只关心原型，而不关系构造函数）

用于构建**多态性**的函数，根据参数类型进行不同的处理。

- `instanceof` 考虑原型链，会不断沿着原型链比较
- `Symbol.hasInstance` 可以自定义 `instanceof` 逻辑
- `obj instanceof Class` 检查等效于 `Class.prototype.isPrototypeOf(obj)`
- `Object.prototype.toString.call()` 检查类型
  - `Symbol.toStringTag` 自定义对象 `toString` 的行为

## Mixin 模式

> JS 中每个对象只能有一个 `[[Prototype]]`，每个类只能扩展另一个类（单继承），`mixins` 帮助将方法添加到类中，而不用继承

Mixin —— 是一个通用的面向对象编程术语：一个包含其他类的方法的类。（可能存在覆盖原有类方法的冲突）

eventMixin 将类型为添加到多个类中，如事件相关的函数

# 对象

对象是一个包含相关数据和方法的集合。对象中的变量和函数被称为属性和方法。每一个属性和值使用键值对的方法表示。
可以添加、修改、删除、访问对象中的任意属性

## 对象属性表示方法

对象的名字表现为一个命名空间 (namespace)
属性可以使用括号或点访问
计算属性：可以在对象字面量中使用方括号，使属性名可以从变量值获取
属性存在测试：

```javascript
alert( "age" in user ); // true，user.age 存在
alert( "blabla" in user ); // false，user.blabla 不存在。
```

`for...in` 遍历对象属性
遍历顺序：整数属性会被进行排序，其他属性则按照创建的顺序显示

- 点表示法

  ```javascript
  person.age
  person.interests[1]
  person.bio()
  ```

- 括号表示法

  ```javascript
  person['age']
  person['name']['first']
  ```

**创建子命名空间：**

```javascript
name : {
  first : 'Bob',
  last : 'Smith'
},

// 访问方法
person.name.first
person.name.last
```

**简写属性值：**

```javascript
function makeUser(name, age) {
  return {
    name, // 与 name: name 相同
    age,  // 与 age: age 相同
    // ...
  };
}
```

**设置对象成员：**

可以更新值，也可以创建

```javascript
person['eyes'] = 'hazel'
person.farewell = function() { alert("Bye everybody!") }
```

**引用和赋值：**
变量赋值对象存储的是对象的引用
拷贝对象变量，拷贝的是对象的引用

**深拷贝:**

- 简单复制 `Object.assign(dest, [src1, src2, src3...])` 拷贝多个对象到目标对象 dest
- 属性是对象引用的情况

## 垃圾回收/内存管理

[JS内存管理](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management)
JavaScript是在创建变量（对象，字符串等）时自动进行了分配内存，并且在不使用它们时“自动”释放

### 垃圾回收算法

- **引用技术垃圾收集**
    > 此算法把“对象是否不再需要”简化定义为“对象有没有其他对象引用到它”。如果没有引用指向该对象（零引用），对象将被垃圾回收机制回收。
    **限制：循环引用**
    IE 6,7 使用，目前基本被淘汰

- **标记-清除算法（基本算法）**
    > 这个算法把“对象是否不再需要”简化定义为“对象是否可以获得”。（解决了循环引用问题）
    **限制：那些无法从根对象查询到的对象都将被清除（实际情况很少碰到）**
    广泛使用

### 可达性

“可达”值是可以通过某种方式可访问或可用的值（一定存储在内存中）

固有可达值基本集合（部分），这些值被称为根`root`：

- 当前执行的函数、其局部变量和参数
- 当前嵌套调用链上的其他函数、其局部变量和参数
- 全局变量
...

一个值可用通过引用链从根访问到任何其他值，则该值可达

### 垃圾回收  JS 引擎优化

- 分代收集：因为代码中许多对象生命周期短，将新老对象根据存活时间长度降低检查频率
- 增量收集：将整个对象集拆分成多个部分，逐步清除，使得对整个对象集的垃圾回收任务形成的大型延迟变成多个小延迟
- 闲时收集：垃圾回收只在CPU空闲时尝试运行

## “this” 的含义

关键字"this"指向了当前代码运行时的对象
“this” 保证了当代码的上下文 (context) 改变时变量的值的正确性

- 方法中的 `this` 指代调用该方法的对象
- `this` 是自由的，不受限制（是实时计算出的，**取决于代码上下文**）
  > **没有对象的情况下调用 `this`**
    严格模式下：`this` 的值为 undefined
    非严格模式下：`this` 将会是全局对象（window）
- 箭头函数没有自己的 `this`（取决于外部的正常函数，即当前上下文）

## 构造器

构造函数：
**大写字母开头** 并且 **由 `new` 操作符执行** 的函数
> `new function() { … }` 立即调用的构造函数
  new.target 属性来检查函数是否被使用 new 调用
  构造函数的 return 值如果是对象，则 new 返回该对象，否则为 this

## symbol 类型

只有 **字符串类型** 和 **symbol类型** 可用作 **对象属性键**

- “symbol” 值表示 **唯一的标识符**。
- 创建时可以给 symbol 一个描述
  `let id = Symbol("id");`
- symbol 值不会被自动转换为字符串
  `id.toString()` 转换为 "Symbol(id)"
  `id.description` 显示描述文字
- 用于创建隐藏属性
  > 对于第三方库，直接添加属性是不安全的（有可能会重写其对象的属性）
- 在对象字面量中使用需要作为变量
  `[id]: 123 // 而不是 "id"：123`
- symbol 属性在对象中不可遍历
  不参与 `for...in` ，被 `Object.keys()` 忽略
  但会被 `Object.assign` 复制

### 全局 symbol

`symbol.for(key)` 方法实现了在代码中调用相同名字的 symbol（创建全局 symbol ）

> 检查全局注册表，如果有一个描述为 key 的 symbol，则返回该 symbol，否则将创建一个新 symbol（Symbol(key)），并通过给定的 key 将其存储在注册表中。

```javascript
// 从全局注册表中读取
let id = Symbol.for("id"); // 如果该 symbol 不存在，则创建它

// 再次读取（可能是在代码中的另一个位置）
let idAgain = Symbol.for("id");

// 相同的 symbol
alert( id === idAgain ); // true
```

`Symbol.keyFor(sym)` 方法实现通过描述反向查找，但 **无法找到非全局 symbol**

系统 symbol ...

### 对象的原始值转换

JS 不允许自定义对象的运算符运算

转换规则

- 布尔值 所有对象均为true
- 数字转换 如 Date 对象可以加减
- 字符转换 如 alert() 等方法实现输出

三种 `hint` 类型决定转换结果，规范明确描述不同运算符选择的 hint 类型

为了进行转换，JavaScript 尝试查找并调用三个对象方法：

1. 调用 obj\[Symbol.toPrimitive](hint) 如果这个方法存在的话
2. 否则，如果 hint 是 "string"
  尝试调用 obj.toString() 或 obj.valueOf()，无论哪个存在。
3. 否则，如果 hint 是 "number" 或 "default"
  尝试调用 obj.valueOf() 或 obj.toString()，无论哪个存在。

使用 `Symbol.toPrimitive` 方法实现转换

```JavaScript
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// 转换演示：
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

`toString/valueOf` 方法在以上不生效的情况下使用

- toString 方法不存在 则调用 valueOf
  普通对象默认返回字符串
- valueOf 方法不存在则调用 toString 方法
  普通对象默认返回对象自身

> **转换可以返回任何类型**，即使数据类型不同
